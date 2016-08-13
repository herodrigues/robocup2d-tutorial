Esta classe faz a leitura das formações do time e também define a [_role_](https://github.com/RoboCup2D/tutorial/blob/master/sections/Roles.md) de cada jogador de acordo com a formação adotada.

Primeiramente, é necessário entender a identificação da área onde a bola está no campo. Na classe Strategy, há um _enum_ para identificar tais áreas:

```cpp
enum BallArea {
        BA_CrossBlock, BA_DribbleBlock, BA_DribbleAttack, BA_Cross,
        BA_Stopper,    BA_DefMidField,  BA_OffMidField,   BA_ShootChance,
        BA_Danger,

        BA_None
    };
```
Conforme a figura abaixo, pode-se entender melhor essa divisão:

![ball-area.png](https://github.com/RoboCup2D/tutorial/raw/master/images/ball-area.png)

Essas demarcações podem ser alteradas posteriormente de acordo com as necessidades da equipe.
Há dois métodos para retornar em qual área a bola está: um com a posição da bola como parâmetro e outro com a visão de mundo do jogador como parâmetro (esse segundo método faz a chamada do primeiro).

```cpp
 static BallArea get_ball_area( const rcsc::WorldModel & wm );
 static BallArea get_ball_area( const rcsc::Vector2D & ball_pos );
```
