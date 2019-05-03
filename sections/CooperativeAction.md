# CooperativeAction

Represents actions to be executed by a group of agents.

The actions categories are:

- Hold - hold the ball
- Dribble - dribble the opponent
- Pass - pass the ball to a teammate
- Shoot - kick the ball to the goal
- Move - move the player
- NoAction - no action

Basically, this class has get and set methods to store information such as players number, action category, action final point, etc.

This class also has a simple struct and a method to compare distances between two points.

```cpp
DistCompare( const rcsc::Vector2D & pos )
            : pos_( pos )
          { }

        bool operator()( const Ptr & lhs,
                         const Ptr & rhs ) const
          {
              return lhs->targetPoint().dist2( pos_ ) < rhs->targetPoint().dist2( pos_ );
          }
```

This method is used to compare distances between two CooperativeAction classes and determine which distance value is greater or lesser than the value between the vector2D targetPoint (action final point) and the point used as parameter in the constructor DistCompare of the struct with the same name. (**See:** dist2 in [Vector2D](https://github.com/RoboCup2D/tutorial/blob/master/sections/Vector2D.md))
