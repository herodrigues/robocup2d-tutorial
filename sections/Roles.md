# Roles

Group of classes to determine the players roles and what they need to do according to their roles and the game strategy.

Each player has a _role_ and this depends on each player position. In the Agend2D code, using the basic formation 4-3-3, the roles are:

![agent2d-basic-formation.png](https://github.com/RoboCup2D/tutorial/raw/master/images/agent2d-basic-formation.png)

- 1 Goalie - Goalkeepr
- 2 CenterBack (left)
- 3 CenterBack (right)
- 4 SideBack (left)
- 5 SideBack (right)
- 6 DefensiveHalf
- 7 OffensiveHalf (left)
- 8 OffensiveHalf (right)
- 9 SideForward (left)
- 10 SideForward (right)
- 11 CenterForward

What do you need to implement is only the behavior of each _role_ in a specific situation.

In the Agent2D, each _role_ has only two methods: doKick() and doMove().

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

The method above checks if the player with the ball possession can kick it to the goal and if the teammate distance to the ball is smaller than the player distance. If these two conditions are met, this means that the player can move with the ball. Otherwise, the player needs to pass the ball to the teammate.

Suppose that you want to perform a through pass. To do that, there is the Bhv_ThroughPassKick class which has the through pass implementation. We also want to perform this pass only with midfielder players (_role_: OffensiveHalf). Then, we need to go to the doKick method in the [RoleOffensiveHalf](https://github.com/RoboCup2D/tutorial/blob/master/sections/RoleOffensiveHalf.md) class and check in which _BallArea_ the player can execute this action.

Remember that, before you implement the behavior, you need to understand how the [Strategy](https://github.com/RoboCup2D/tutorial/blob/master/sections/Strategy.md) class works.

For example:
```cpp
//[...]
switch ( Strategy::get_ball_area( agent->world().ball().pos() ) ) {
    case Strategy::BA_OffMidField:

        if(Bhv_ThroughPassKick().execute(agent))
	    break;
        // other actions
        break;

    //[...] case n:
}
```

The player will only execut the through pass if the ball is in the offensive midfield (BA_OffMidField) and if the Bhv_ThroughPassKick's execute method returns true. That is, if the player can really execute this action. If the ball is in the BA_OffMidField area but the player has no condition of executing the pass through, then another action will be executed.
