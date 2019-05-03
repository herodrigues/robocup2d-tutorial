# Line2D

**rcsc/geom/line_2d.h**

Represents the linear equation: `aX + bY + c = 0`.
This class is very useful to calculate the players or the ball path and check if a point or line intercepts another line.

![line2d.png](https://github.com/RoboCup2D/tutorial/raw/master/images/line2d.png)

Some methods of this class:
```cpp
// calculates the Euclidian distance of a point to this line
double dist( const Vector2D & p ) const         

// check if this line is parallel to another line
bool isParallel( const Line2D & line ) const    

// returns the intersection point of this line with another line
Vector2D intersection( const Line2D & line ) const     

// returns the perpendicular line to this line starting from a specific point
Line2D perpendicular( const Vector2D & p ) const       

// returns the intersection point of two lines
static Vector2D intersection( const Line2D & line1, const Line2D & line2 );   

// returns the angle bisector
static Line2D angle_bisector( const Vector2D & origin, const AngleDeg & left, const AngleDeg & right )

```

**References**:
- Angle Bisector - http://mathworld.wolfram.com/AngleBisector.html
- Linear Equation - http://mathworld.wolfram.com/LinearEquation.html
