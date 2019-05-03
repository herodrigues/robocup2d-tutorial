# Strategy

This class reads the team formations and also defines each player [_role_](https://github.com/RoboCup2D/tutorial/blob/master/sections/Roles.md) according to the adopted formation.

First, it is necessary to understand the naming convention used to determine where the ball is in the field. There is a _enum_ to identify such areas:

```cpp
enum BallArea {
        BA_CrossBlock, BA_DribbleBlock, BA_DribbleAttack, BA_Cross,
        BA_Stopper,    BA_DefMidField,  BA_OffMidField,   BA_ShootChance,
        BA_Danger,

        BA_None
    };
```

This field division can be visualized in the image below:

![ball-area.png](https://github.com/RoboCup2D/tutorial/raw/master/images/ball-area.png)

These areas can be modified according to the team needs.

There are two methods to return the ball area:
- using the ball position as parameter
- using the player world model 

```cpp
 static BallArea get_ball_area( const rcsc::WorldModel & wm );
 static BallArea get_ball_area( const rcsc::Vector2D & ball_pos );
```
