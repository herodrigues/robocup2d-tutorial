This is probably the most important class to understand how Agent2D works. As the name says for it self, this class is responsible for analyzing the field using a Voronoi Diagram to decide which action should be taken by the agent.

A brief explanation of a Voronoi Diagram can be found in this video:
https://www.youtube.com/watch?v=Q804hv73L6U

To understand how this diagram is implemented, see the class [Voronoi Diagram](https://github.com/RoboCup2D/tutorial/blob/master/sections/VoronoiDiagram.md).


In [SamplePlayer](https://github.com/RoboCup2D/tutorial/blob/master/sections/SamplePlayer.md)'s actionImpl(), which is called in every game cycle, an instance of FieldAnalyzer is called too. Before this call, methods related to game strategy are also used (see [Strategy](https://github.com/RoboCup2D/tutorial/blob/master/sections/Strategy.md))


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

Before generating a chain of actions, the field is analyzed at every game cycle. Note that is very important that you've grasped the concept of a Voronoi Diagram. The SamplePlayer class has the following source:

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

You can see that the method responsible for updating the Voronoi Diagram is commented out. **More tests need to be done to know exactly what this method does**. 
This method excludes some game modes in which the diagram is not analyzed. They are BeforeKickOff, AfterGoal_ e isPenaltyKickMode.
