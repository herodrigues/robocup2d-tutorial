# Vector2D

**rcsc/geom/vector_2d.h**

This class represents a point in a 2D space.

![vector2d.png](https://github.com/RoboCup2D/tutorial/raw/master/images/vector2d.png)

Where _O_ is the origin, that is, the field center. Do not forget that the y axis is inverted in the simulator. Thus, the quadrant in which the point is on the image below is positive (x, y).

The points are:
```cpp
double x; // point in X
double y; // point in Y

// default constructor
Vector2D() : x( 0.0 ), y( 0.0 ) { }

// assignment constructor
Vector2D( const double & xx, const double & yy ) : x( xx ), y( yy ) { }
```

There are several utility methods on this class, so do not waste your time trying to rewrite them. To see them all, look for `rcsc/geom/vector_2d.h` in the same folder librcsc was installed. There's a brief explanation for all methods in that file.

The Vector2D parameter used in the methods below will use the Vector2D parameters passedn in the constructor as the origin.

```cpp
double r2() const      // squared value
double r() const       // distance
double norm() const    // normalized value 
double norm2() const   // squared normalized value
double length() const  //
double length2() const // squared length
AngleDeg th() const    // angle relative to the point
AngleDeg dir() const   
Vector2D abs() const   // absolute value 
double absX() const    // absolute value of x
double absY() const    // absolute value of y
Vector2D & add( const Vector2D & v )                    // sum two Vector2D points
Vector2D & add( const double & xx, const double & yy )  // sum (x, y) to a Vector2D point
Vector2D & scale( const double & scalar )               // scalar multiplication
double dist2( const Vector2D & p ) const   // squared distance from p (x1-x2)² + (y1-y2)²
double dist( const Vector2D & p ) const    // Euclidian distance from p √((x1-x2)² + (y1-y2)²)

bool equals( const Vector2D & other ) const // checks equal distance to a Vector2D point 
Vector2D & rotate( const double & deg )     // rotates a Vector2D using an angle value deg (returns the pointer reference)
Vector2D & rotate( const AngleDeg & angle ) // rotates a Vector2D using an angle of type AngleDeg (returns a new Vector2D)
Vector2D & setDir( const AngleDeg & dir )   // sets an angle to a Vector2D
```

You can check this library for more methods such as printing, comparison, division, subtraction, etc.
