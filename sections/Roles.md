Conjunto de classes para definir qual a função do jogador e o que ele deve fazer de acordo com sua função e estratégia do jogo.

Cada jogador tem uma _role_ e isso depender da posição jogador. No código do Agent2D 3.1.1, existem as seguintes _roles_ na formação básica 4-3-3 conforme a figura abaixo:

![agent2d-basic-formation.png](https://github.com/RoboCup2D/tutorial/raw/master/images/agent2d-basic-formation.png)

_1 Goalie - Goleiro_

_2 CenterBack - Zagueiro central_

_3 CenterBack - Zagueiro central_

_4 SideBack - Lateral esquerdo_

_5 SideBack - Lateral direito_

_6 DefensiveHalf - Volante_

_7 OffensiveHalf - Meio-campo ofensivo (esquerdo)_

_8 OffensiveHalf - Meio-campo ofensivo (direito)_

_9 SideForward - Ponta esquerdo_

_10 SideForward - Ponta direito_

_11 CenterForward - Centroavante_



O que você desenvolverá são apenas Behaviours (comportamentos) para cada _role_ em determinada situação. 

**No código original** do Agent2D, cada _role_ tem apenas dois métodos: doKick() e doMove(). Vejamos:
```cpp
bool
RoleCenterBack::execute( PlayerAgent * agent )
{
    bool kickable = agent->world().self().isKickable();
    if ( agent->world().existKickableTeammate()
         && agent->world().teammatesFromBall().front()->distFromBall()
         < agent->world().ball().distFromSelf() )
    {
        kickable = false;
    }

    if ( kickable )
    {
        doKick( agent );
    }
    else
    {
        doMove( agent );
    }
    
    return true;
}
```
O método acima verifica se o jogador que está com a bola tem condições de chutá-la e se a distância dos companheiros de equipe para a bola é menor que sua própria distância. Se estas duas condições forem satisfeitas, isso indica que o jogador deve se mover com a bola, caso contrário, ele deve passar a bola para um companheiro de equipe.

Vamos supor que se queria testar o passe em profundidade. Para isso, temos o Bhv_ThroughPassKick onde está implementado todo o cálculo do passe em profundidade.
Ainda, queremos fazer o passe somente com os jogadores ofensivos de meio-campo (_role_: OffensiveHalf). Então, basta ir no método doKick() da classe [RoleOffensiveHalf](https://github.com/RoboCup2D/tutorial/blob/master/sections/RoleOffensiveHalf.md) e verificar em quais _BallArea's_ o jogador pode executar o passe em profundidade. 

Lembre-se, antes de implementar seu behaviour, você deve entender como funciona a classe [Strategy](https://github.com/RoboCup2D/tutorial/blob/master/sections/Strategy.md).

Por exemplo:
```cpp
//[...]
switch ( Strategy::get_ball_area( agent->world().ball().pos() ) ) {
    case Strategy::BA_OffMidField:
       
        if(Bhv_ThroughPassKick().execute(agent))
	    break;
        // outras situações
        break;

    //[...] case n:
}
```
Nesse exemplo, o jogador só irá executar o passe em profundidade se a bola estiver no meio-campo ofensivo (BA_OffMidField) e se o método execute() da classe Bhv_ThroughPassKick retornar true, ou seja, uma condição favorável ao passe. Caso a bola esteja em BA_OffMidField mas o jogador não tenha condições de fazer o passe em profundidade, ele executará outra ação (outro tipo de passe).
