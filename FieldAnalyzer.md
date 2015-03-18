Provavelmente, a classe mais importante para entender o funcionamento do agent2D. É ela que vai, literalmente, analisar o campo a partir do diagrama de Voronoi para então decidir que ação deve ser tomada pelo agente.

Uma explicação bem simples do diagrama de Voronoi pode ser encontrada aqui: 
http://www.ime.usp.br/~freitas/gc/voronoi.html

Para entender o funcionamento do código do diagrama de Voronoi da librcsc, veja a classe [Voronoi Diagram](https://bitbucket.org/herinson/ibots2d/wiki/VoronoiDiagram).

No método actionImpl() do [SamplePlayer](https://bitbucket.org/herinson/ibots2d/wiki/SamplePlayer) (que é chamado a cada ciclo do jogo), a instância da classe FieldAnalyzer é chamada já na segunda linha. Antes dela, a chamada responsável pela estratégia de jogo também atualizada. (Mais detalhes, veja a classe [Strategy](https://bitbucket.org/herinson/ibots2d/wiki/Strategy)).

```cpp
void
SamplePlayer::actionImpl()
{
    //
    // update strategy and analyzer
    //
    Strategy::instance().update( world() );
    FieldAnalyzer::instance().update( world() );

   //[...]
```
Antes da cadeia de ações ser gerada, o campo é analisado a cada ciclo. Note que nesse ponto, é muito importante que você tenha entendido o diagrama de Voronoi.

A chamada feita no SamplePlayer tem o seguinte código na classe FieldAnalyzer:
```cpp
void
FieldAnalyzer::update( const WorldModel & wm )
{
    static GameTime s_update_time( 0, 0 );

    if ( s_update_time == wm.time() )
    {
        return;
    }
    s_update_time = wm.time();

    if ( wm.gameMode().type() == GameMode::BeforeKickOff
         || wm.gameMode().type() == GameMode::AfterGoal_
         || wm.gameMode().isPenaltyKickMode() )
    {
        return;
    }
    
#ifdef DEBUG_PRINT
    Timer timer;
#endif

    //updateVoronoiDiagram( wm );

#ifdef DEBUG_PRINT
    dlog.addText( Logger::TEAM,
                  "FieldAnalyzer::update() elapsed %f [ms]",
                  timer.elapsedReal() );
    writeDebugLog();
#endif
```
O trecho do código onde é chamado o método que, de fato, atualiza o diagrama de Voronoi vem comentado no código original do agent2D. **Testes precisam ser feitos para analisar o impacto desse método**. 
Seguindo o resto da lógica, basicamente, esse método exclui algumas situações onde o diagrama não é atualizado, são elas início e retomada do jogo e nos seguintes modos de jogo: BeforeKickOff, AfterGoal_ e isPenaltyKickMode.