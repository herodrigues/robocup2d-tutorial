# Vector2D

**rcsc/geom/vector_2d.h**

Essa classe possui métodos de extrema importância para o entendimento do simulador, pois ela armazena dois pontos no espaço bidimensional e isso é a chave da simulação 2D de futebol.

Um Vector2D nada mais é que um vetor em um espaço bidimensional como mostrado na figura:

![vector2d.png](https://github.com/RoboCup2D/tutorial/raw/master/images/vector2d.png)

Onde _O_ é a origem, ou seja, o centro do campo. Não se esqueça que no eixo de coordenadas do simulador, o eixo y é invertido. Portanto, o quadrante onde se encontra os pontos da figura é x e y positivo.

Os pontos no plano são representados por:
```cpp
double x; // coordenada X
double y; // coordenada Y

// construtor padrão
Vector2D() : x( 0.0 ), y( 0.0 ) { }

// construtor para associar valores diretamente
Vector2D( const double & xx, const double & yy ) : x( xx ), y( yy ) { }
```

Apesar de simples, os metódos listados aqui são bastante úteis e evitam que você desperdice tempo codificando métodos que já existam. Para ver todos, procure o arquivo rcsc/geom/vector_2d.h no diretório onde você instalou a librcsc, lá todos os métodos possuem uma breve explicação.

Nos exemplos abaixo, o vector2D passado como parâmetro vai ser comparado com a instância que você criou da classe vector2D:

```cpp
double r2() const      // retorna o valor ao quadrado
double r() const       // retorna o tamanho
double norm() const    // retorna o valor normalizado ( equivalente ao método r() )
double norm2() const   // retorna o valor normalizado ao quadrado ( equivalente ao método r2() )
double length() const  // retorna o tamanho ( equivalente ao método r() )
double length2() const // retorna o valor ao quadrado do tamanho ( equivalente ao método r2() )
AngleDeg th() const    // retorna o ângulo
AngleDeg dir() const   // retorna o ângulo ( equivalente ao método th() )
Vector2D abs() const   // retorna os valores absolutos
double absX() const    // retorna o valor absoluto de x
double absY() const    // retorna o valor absoluto de y
Vector2D & add( const Vector2D & v )                    // adiciona os valores x e y de v ao vetor
Vector2D & add( const double & xx, const double & yy )  // adiciona específicos valores para x e y
Vector2D & scale( const double & scalar )               // multiplicação de x e y por escalar
double dist2( const Vector2D & p ) const   // retorna a distância ao quadrado com o ponto 'p' (x1-x2)² + (y1-y2)²
double dist( const Vector2D & p ) const    // retorna a distância euclidiana com o ponto 'p' √((x1-x2)² + (y1-y2)²)

bool equals( const Vector2D & other ) const // checa se a distância do vector2D é exatamente idêntico ao outro
Vector2D & rotate( const double & deg )     // rotaciona o vector2D com o valor do ângulo 'deg' (retorna a referência)
Vector2D & rotate( const AngleDeg & angle ) // rotaciona o vector2D com o ângulo do tipo AngleDeg (retorna um novo vector2D)
Vector2D & setDir( const AngleDeg & dir )   // atribui um ângulo ao vector2D
```

Além desses metódos básicos, existem diversos métodos de comparação, print e operações aritméticas como soma, divisão, subtração, etc.
