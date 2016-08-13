**rcsc/geom/line_2d.h**

Classe que representa a fórmula linear aX + bY + c = 0. 
Muito últi para calcular trajetórias de jogadores ou da bola e para verificar se um ponto ou uma reta intercepta outra reta.

A imagem abaixo mostra uma reta no plano bidimensional e um ponto perpendicular à ela:

![line2d.png](https://github.com/repo/qM7nyp/images/202542245-line2d.png)

Métodos úteis dessa classe:
```cpp
double dist( const Vector2D & p ) const         // calcula distância euclidiana de um ponto para esta reta
bool isParallel( const Line2D & line ) const    // verifica se uma reta é paralela a esta reta
Vector2D intersection( const Line2D & line ) const     // retorna o ponto de intersecção desta reta com outra
Line2D perpendicular( const Vector2D & p ) const       // retorna a reta perpendicular à outra a partir de um ponto específico
static Vector2D intersection( const Line2D & line1, const Line2D & line2 );   // retorna o ponto de 
                                                                              // intersecção de duas retas
static Line2D angle_bisector( const Vector2D & origin, const AngleDeg & left, const AngleDeg & right )
                                                                        // retorna a bissetriz de um ângulo
```

**Referências**: 
Ângulo bisector - http://mathworld.wolfram.com/AngleBisector.html 
Equação da reta - http://mathworld.wolfram.com/LinearEquation.html 