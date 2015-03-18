Classe com funções matemáticas.

Abaixo estão listados alguns dos métodos dessa classe:

```cpp
// limita um valor dentro de um intervalo
template < typename  T > const T & bound( const T & low, const T & x, const T & high )

// calcula o quadrado de um número
template < typename T > T square( const T & x )

// retorna se o sinal de um número 
inline double sign( const double & x )

// arredonda um valor de ponto flutuante com uma precisão específica
inline double round( const double & value, const double & prec )

// fórmula de Bhaskara, retorna o número de soluções
inline int quadratic_formula( const double & a, const double & b, const double & c, double * sol1, double * sol2 )

// calcula a soma de uma série geométrica
inline double calc_sum_geom_series( const double & first_term, const double & r, const int len )

// calcula a soma de séries geométricas infinitas
inline double calc_sum_inf_geom_series( const double & first_term, const double & r )


```
