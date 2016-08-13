**rcsc/geom/ray_2d.h**

Classe para representação de um raio traçado a partir de uma origem _O_ qualquer.

Por exemplo, pode ser utilizada quando se deseja analisar se existe algum adversário no raio que se forma entre um jogador e a bola ou qualquer outro ponto.

![ray_2d.gif](https://github.com/RoboCup2D/tutorial/raw/master/images/ray_2d.gif)

Métodos úteis:
```cpp
Vector2D intersection( const Line2D & other ) const   // retorna o ponto de intersecção com uma reta (Line2D)
Vector2D intersection( const Ray2D & other ) const    // retorna o ponto de intersecção com um raio (Ray2D)
Line2D line() const    // retorna a reta gerada pelo raio
```
