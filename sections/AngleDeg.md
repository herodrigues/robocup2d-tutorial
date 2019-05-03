# AngleDeg

**rcsc/geom/angle_deg.h**

This class converts angles to degrees. As we all know, the mathematic functions in ANSI C are represented in radians. Thus, this class is extremely important in several calculations during the match.

![](https://raw.githubusercontent.com/robocup2d/robocup2d/master/images/polar_coordinate_system.png)

In the picture above, if we have a point *P* in _P(4, 3)_, then the angle *φ* will be:
```latex
r² = 4² + 3²
r = sqrt(25)
r = 5

sin φ = 25 / r
sin φ = 25 / 5
φ ≃ 2.78 rad ou φ ≃ -55.59º
```

Useful methods on this class:
```cpp
// normalize angles in the interval [-180°, 180°]
const AngleDeg & normalize()  

// returns the absolute angle value
double abs() const            

// returns the angle value in radians
double radian() const          
```

This class has several other useful methods such as sin, tangent, arctangent and radians, besides overloading of arithmetical operators.
