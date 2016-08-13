Nessa seção é descrito o sistema de formação SBSP (*Situation Based Strategic Positioning* ou em português algo como Posicionamento Estratégico Baseado na Situação). Nesse SBSP, cada player agent não é considerado no movimento dos outros jogadores e para a posição-alvo do movimento é considerada como entrada somente a posição da bola. Isto é feito para apenas parecer que não é um posicionamento cooperativo, e sim como em uma coordenação aparentemente individual.
O comportamento de posicionamento descrito nesta seção é algo próximo às habilidades individuais de cada player agent. No entanto, uma vez que são necessários ajustes em consideração ao equilíbrio de toda a equipe na implementação da operação, o que se segue aqui é uma parte da seção Desenvolvimento da Equipe.

### Marcando o jogador adversário ###

A marcação próxima a um adversário específico é necessária quando o time está em seu campo de defesa. Obviamente, essa operação pode ser feita em outras situações, mas isso pode acarretar em um uso excessivo de stamina do jogador. Porém, isto necessariamente não leva à uma situação perigosa de jogo que poderia atrapalhar a formação do time. Estando no campo adversário e sem bola, uma marcação à distância já é suficiente.
Com a posse de bola, uma marcação no campo de defesa pode trazer problemas ao tentar receber a bola em um passe; porém, no seu campo de ataque e estando sem a bola, isto será o objetivo principal desse comportamento. Para conseguir isto, mais do que marcar o adversário desejado é necessário mover-se próximo à posição da bola.
Antes de decidir a posição-alvo do movimento de marcação, primeiro é necessário determinar qual jogador adversário será marcado. No código a seguir, decide-se qual jogador adversário será o candidato:

```cpp
const PlayerObject * getMarkTarget( const WorldModel & wm, const Vector2D & home_pos ) 
{
	double dist_opp_to_home = 1000.0;
	const PlayerObject * opp = wm.getOpponentNearestTo( M_home_pos, 1, &dist_opp_to_home );

	if ( ! opp || ( wm.existKickableTeamamte() && opp->distFromBall() > 2.5 ) ) {
		return NULL;
	}
	if ( dist_opp_to_home > 7.0 && home_pos.x < opp->pos().x ) {
		return NULL;
	}
	const PlayerPtrCont::const_iterator
	end = wm.getTeammatesFromSelf().end();

	for ( PlayerPtrCont::const_iterator it = wm.getTeammatesFromSelf().begin(); it != end; ++it ) {
	    if ( (*it)->pos().dist( opp->pos() ) < dist_opp_to_home ) {
	        return NULL;
            }
	}
	return opp;
}
```

O código acima determina a posição para onde o player agent deve realizar o movimento de marcação sobre o adversário que, consequentemente, torna-se o jogador-alvo (target player).

Obtendo-se um ponteiro para o PlayerObject do adversário no método getMarkTarget, uma última modificação na coordenada Y é necessária para retroceder sem precisar de nenhuma rotação extra. Aqui, utiliza-se o valor da posição Y do próprio agent player, mas você pode utilizar um valor fixo.

```cpp
AngleDeg block_angle = ( wm.ball().pos() - opp->pos() ).th();
Vector2D block_point = opp->pos() + Vector2D::polar2vector( 0.2, block_angle );
block_point.x -= 0.1;

if ( block_point.x < wm.self().pos().x - 1.5 ) {
    block_point.y = wm.self().pos().y;
}
```

No trecho de código acima, o objetivo é marcar o adversário próximo à home position do player agent. Numa visão mais abrangente onde se deseja um equilíbrio entre a função de cada jogador, a formação do time e os outros companheiros de equipe, seria necessária uma marcação mais complexa. Porém, em se tratando apenas de elaboração de regras, marcar o adversário parecer ser um tanto quanto difícil, particularmente, quando informações para identificação de outros jogadores são insuficientes. 
Portanto, para conseguir um comportamento de marcação mais confiável, compartilhar informações através de comunicação entre os jogadores é essencial.

### Bloquear a linha de passe  ###

Bloquear a linha de passe é uma importante tática defensiva pois reduz-se as opções do time adversário. Porém, como o jogador que está com a bola toma a iniciativa da jogada, o path behaviour não permite que o path course seja bem bloqueado mesmo se um player agent com características bem balanceadas for utilizado para tentar o bloqueio. Além disso, como a bola se move rapidamente, nem sempre é necessário tentar bloquear a linha de passe pois será difícil acompanhar o movimento da bola. Consequentemente, semelhante ao comportamento de marcação, é melhor tentar bloquear a linha de passe em situações defensivas onde o time está em seu campo de defesa.


O código a seguir mostra como bloquear a linha de passe da frente do gol até a direção do escanteio.

```cpp
const BallObject & ball = agent->world().ball();
Vector2D center( -41.5, 0.0 );

if ( ball.pos().x < -45.0 ) {
    center.x = std::max( -48.0, ball.pos().x + 1.0 );
}

Line2D block_line( wm.ball().pos(), ( center - wm.ball().pos() ).th() );
Vector2D block_point;
block_point.y = std::max( 15.0, ball.pos().absY() - 10.0 );

if ( ball.pos().y < 0.0 ) block_point.y *= -1.0;
block_point.x = block_line.getX( block_point.y );
```

No exemplo acima, o player agent foi designado a mover-se em uma linha reta estabelecida entre uma posição fixa na frente do centro do gol e a posição da bola. Á 10m da bola, a distância mínima do eixo Y é 15m da coordenada Y da posição de bloqueio (block_point). Note que a role do jogador deve adotar outras regras quando o valor da coordenada Y da posição da bola é 15m ou menos. A coordenada X pode ser calculada a partir da equação da reta e o valor da coordenada Y.
Essa implementação não pode ser considerada ótima pois nela é usado um número mágico, assim como em implementações similares a esta.

Se você deseja bloquear a linha de passe de jogadores adversários em particular, o player agent deve se mover na linha reta que conecta o adversário e a bola. Porém, a posição-alvo do movimento irá mudar durante os ciclos considerando que a bola e o adversário irão se mover.
Durante o bloqueio, determinar se a posição do movimento é boa de uma forma fixa trará mais resultados do que apenas tentar bloquear uma linha reta qualquer do passe.

### Marcação na frente do adversário ###

Imagine uma situação onde o jogador adversário inica um drible. Você não pode simplesmente correr atrás dele e tentar roubar a bola executando um behaviour para interceptar o drible.
Nesse caso, é necessário que haja uma marcação na frente do adversário.

Segue o código: 

```cpp
const WorldModel & wm = agent->world();
const PlayerObject * opp = wm.interceptTable()->fastestOpponent();

if ( ! opp ) {
    return;
}
Vector2D block_point = opp->pos();

if ( wm.self().pos().x > opp->pos().x ) {
    block_point.x -= 5.0;
} else {
    block_point.x -= 2.0;
}

Body_GoToPoint( block_point,
     1.0, // 1m para o erro da distância
     ServerParam::i().maxPower(),
     5, // de modo a atingir a posição de destino depois de cinco ciclos
     false, // não usar dash para trás
     true, // não consumir recover
     40.0 //  permitir até 40 graus de erro de direção 
).execute( agent );
```

Você deve estar imaginando que o código acima para obter a posição-alvo é bem simples. De fato, é bem simples. Contudo, a intenção não é ir exatamente no ponto onde previu-se o movimento do jogador adversário. 
Além do mais, o código acima pode resultar em rotações desnecessárias quando elaborado apenas para um ponto. Para resolver isto, basta atribuir um valor de erro maior no método BodyGoToPoint. Como resultado, é possível reduzir as rotações desnecessárias apenas mudando um pouco a direção da posição-alvo.

Prever o comportamento do adversário pode ser mais eficaz quando executado pelos jogadores ofensivos.

### Movimento para cancelar a marcação ###

1. Busca dinâmica

Existem vários métodos para calcular o campo potencial como uma forma de mudar a posição do movimento. O código a seguir obtém a densidade do jogador em uma certa posição.


```cpp
Vector2D target_point( 45.0, 0.0 );
double congestion = 0.0;
const PlayerPtrCont::const_iterator end = agent->world().getOpponentsFromSelf().end();

for ( PlayerPtrCont::const_iterator o = agent->world().getOpponentsFromSelf().begin(); o != opps_end; ++o ) {
    congestion += 1.0 / (*o)->pos().dist2( target_point );
}
```

No exemplo acima, é obtida a densidade de congestão dos jogadores adversários em um ponto específico (target_point). A posição que o valor da congestão possui é minimizado de acordo com o cálculo de várias coordenadas de posições medidas a partir do target_point.

Tudo parece ótimo nessa algoritmo, mas não funciona nesse caso. O campo de visão do player agent é limitado e desde que cada jogador está se movendo, as posições-alvo (target position) dos jogadores adversários estão constantemente mudando. Nesse caso, operações de rotaçãoes incluíram vários movimentos do player agent e isto não seria nada eficiente.

Uma solução para isto é registrar a intenção de movimento do tempo limite em uma forma que continue a realizar operações de movimentação para a posição, assim em um certo período de tempo você pode decidir qual target position será escolhida de acordo com o tempo considerado.

No entanto, mesmo reduzindo movimentos utilizando intention, mudanças dinâmicas da posição-alvo que está em movimento parece não surtir muito efeito. Se você deseja um efeito mais confiável, é melhor usar um método que incorpore regras estáticas que serão descritos abaixo.


```cpp
const WorldModel & wm = agent->world();
Vector2D target_point = home_pos;

if ( wm.ball().pos().y * wm.self().pos().y < 0.0 && wm.ball().pos().x > 40.0 
       && 6.0 < wm.ball().pos().absY() && wm.ball().pos().absY() < 17.0 ) {

    Rect2D goal_area( Vector2D( 52.5 - 8.0, -6.0 ),
    Vector2D( 52.5, 6.0 ) );

    if ( ! wm.existTeammateIn( goal_area, 10, true ) ) {
        target_point.x = wm.ball().pos().x + 2.0;
        
        if ( target_point.x > wm.getOffsideLineX() - 1.0 ) {
            target_point.x = wm.getOffsideLineX() - 1.0;
        }
    
        if ( target_point.x > 49.0 ) target_point.x = 49.0;
        target_point.y = -1.0;
        if ( wm.ball().pos().y > 0.0 ) target_point.y *= -1.0;
    }
}
```

Você também pode realizar a operação para cancelar a marcação através de regras de posicionamento fixo. Desta forma, é possível determinar a posição fixa do target point. Para ser mais preciso, isto não é um posicionamento dinâmico, isto é um posicionamento tático para uma situação local, como será explicado na mais detalhadamente na próxima seção.
Por exemplo, no caso da role ForwardSide, o que você deve fazer é passar para a frente do gol para marcar o adversário de frente como mostrado no código a seguir.

```cpp
const WorldModel & wm = agent->world();
Vector2D target_point = home_pos;

if ( wm.ball().pos().y * wm.self().pos().y < 0.0 && wm.ball().pos().x > 40.0
       && 6.0 < wm.ball().pos().absY() && wm.ball().pos().absY() < 17.0 ) {

	Rect2D goal_area( Vector2D( 52.5 - 8.0, -6.0 ),
	Vector2D( 52.5, 6.0 ) );

	if ( ! wm.existTeammateIn( goal_area, 10, true ) ) {
		target_point.x = wm.ball().pos().x + 2.0;
		if ( target_point.x > wm.getOffsideLineX() - 1.0 ) {
		    target_point.x = wm.getOffsideLineX() - 1.0;
		}
		if ( target_point.x > 49.0 ) target_point.x = 49.0;
		target_point.y = -1.0;
		if ( wm.ball().pos().y > 0.0 ) target_point.y *= -1.0;
	}
}
```

### Ajuste da orientação do corpo do player agent ###

A melhor ideia durante o jogo é ajustar a orientação do corpo mesmo quando não há ação a ser feita, em particular, quando o jogador já atingiu a posição final do seu movimento.
Para um jogador ofensivo, é suficiente apenas rodar o corpo para a direção da linha de gol adversário. Isso pode ser facilmente obtido com o código a seguir:

```cpp
if ( ! Body_GoToPoint( target_point, dist_thr, dash_power).execute( agent ) ) {
    Vector2D face_point( 100.0, wm.self().pos().y );
    Body_TurnToPoint( face_point ).execute( agent );
}
```
Além disso, é útil ajustar a posição através do rear dash sem precisar mudar a orientação do corpo quando um jogador com role de marcação mais agressiva tiver que se mover continuamente para a target position.

```cpp
if ( wm.self().pos().x > target_point.x + dist_thr*0.5 
    && std::fabs( wm.self().pos().x - target_point.x ) < 3.0 && wm.self().body().abs() < 10.0 ) {

    double back_dash_power = wm.self().getSafetyDashPower( -dash_power );
    agent->doDash( back_dash_power );
}
```

Para um jogador com role defensiva, é necessário elaborar quase que um "comportamento racional" de interceptação. Por exemplo, no caso de uma role que faz uma linha defensiva a interceptação, considerando que é necessário o movimento que interfira o curso de movimento do jogador adversário de lado a lado, é mostrado no código a seguir: 

```cpp
if ( ! Body_GoToPoint( target_point, dist_thr, dash_power ).execute( agent ) ) {
    Vector2D face_point( wm.self().pos().x, 0.0 );
    face_point.y = ( wm.ball().pos().y < wm.self().pos().y ? -40.0 : 40.0 );
    Body_TurnToPoint( body_point ).execute( agent );
}
```

Além disso, você precisará armazenar a direção perpendicular do corpo do player agent em relação à bola de modo que ficar fácil de lidar caso ela seja chutada de repente:

```cpp

if ( ! Body_GoToPoint( target_point, dist_thr, dash_power ).execute( agent ) ) {
    AngleDeg body_angle = wm.ball().angleFromSelf();
   
    if ( body_angle.degree() < 0.0 ) body_angle -= 90.0;
    else body_angle += 90.0;
  
    Vector2D face_point = wm.self().pos();
    face_point += Vector2D::polar2vector( 10.0, body_angle );
    Body_TurnToPoint( face_point ).execute( agent );
}
```

Porém, você deve verificar a posição da bola em qualquer caso. Assim, a operação para ajustar a orientação do corpo deve ser executada somente quando for possível confirmar a posição da bola.