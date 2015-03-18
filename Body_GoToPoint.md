**rcsc/action/body_go_to_point.h**

```cpp
#include "strategy.h"
#include <rcsc/action/body_go_to_point.h>
// [...]
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

#if 0
    if ( kickable )
    {
        doKick( agent );
    }
    else
    {
        doMove( agent );
    }
#endif
    
    doMove( agent );
    return true;
}
// [...]
void
RoleCenterBack::doMove( PlayerAgent * agent )
{
    const WorldModel & wm = agent->world();
    const Vector2D target = Vector2D(0, 0);
    const double dash_power = Strategy::get_normal_dash_power( wm );
    
    double dist_thr = wm.ball().distFromSelf() * 0.1;
    
    if( dist_thr < 1.0 ) dist_thr = 1.0;
    
    agent->debugClient().addCircle( target, dist_thr );
    agent->debugClient().setTarget( target );
    
    Body_GoToPoint( target, dash_power, dist_thr ).execute( agent );
}
```