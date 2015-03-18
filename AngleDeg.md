**rcsc/geom/angle_deg.h**

Classe que representa ângulos em graus. Como bem se sabe, as funções matemáticas presentes no ANSI C são apenas para radianos, portanto, o uso dessa classe é de extrema importância em diversos cálculos durante uma partida.


![polar_coordinate_system.png](https://bitbucket.org/repo/qM7nyp/images/4043523102-polar_coordinate_system.png)


Na imagem acima, se considerarmos o ponto _P_ como sendo _P(4, 3)_ logo teremos o valor do ângulo φ igual a:
```matlab
r² = 4² + 3²
r = sqrt(25)
r = 5

sin φ = 25 / r
sin φ = 25 / 5
φ ≃ 2.78 rad ou φ ≃ -55.59º
```

Métodos úteis dessa classe:
```cpp
const AngleDeg & normalize()   // normaliza o ângulo no intervalo [-180º, 180º]
double abs() const             // retorna o valor absoluto do ângulo
double radian() const          // retorna o valor do ângulo em radianos
```
Essa classe possui muitos outros métodos úteis como cosseno, seno, tangente, arco-tangente, entre outros em graus e radianos, além de sobrecarga de operadores aritméticos, 