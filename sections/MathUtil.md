# MathUtil

Mathematical helper methods

```cpp
// limit a value in a interval
template < typename  T > const T & bound( const T & low, const T & x, const T & high )

// square value of a type
template < typename T > T square( const T & x )

// returns th signal of a double
inline double sign( const double & x )

// round the value of a double with a precision value
inline double round( const double & value, const double & prec )

// Quadratic equation: returns the number of solutions
inline int quadratic_formula( const double & a, const double & b, const double & c, double * sol1, double * sol2 )

// calculates the sum of a geometric series
inline double calc_sum_geom_series( const double & first_term, const double & r, const int len )

// calculate the sum of infinite geometric series
inline double calc_sum_inf_geom_series( const double & first_term, const double & r )

```
