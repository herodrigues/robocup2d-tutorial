# SoccerMath

This class has a method that can be modified to improve the kick algorithm.

```cpp
/*!
  \brief Calculates the kick rate
  \param dist Distance between the player and the ball
  \param dir_diff Difference between the player angle and the ball
  \param kprate Player kick rate power
  \param bsize Ball ray
  \param psize Player ray
  \param kmargin Player's kickable area margin
  \return Power kick rate 
*/
inline double kick_rate( const double & dist,
           const double & dir_diff,
           const double & kprate,
           const double & bsize,
           const double & psize,
           const double & kmargin )
```
