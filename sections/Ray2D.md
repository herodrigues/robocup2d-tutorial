# Ray2D

**rcsc/geom/ray_2d.h**

Represents the ray from any origin _O_.

It can be useful when one needs to analyse if any opponent is inside the ray between the ball and any other player (or any other point)

![ray_2d.gif](https://github.com/RoboCup2D/tutorial/raw/master/images/ray_2d.gif)

Useful methods:
```cpp
// returns the intersection point with a line
Vector2D intersection( const Line2D & other ) const

// returns the intersection point with a ray
Vector2D intersection( const Ray2D & other ) const

// returns the generated line by the ray
Line2D line() const
```
