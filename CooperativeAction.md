Classe que representa ações para serem tomadas em grupo por um agente.

As categorias de ações são:

Hold - segurar a bola 
Dribble - driblar o adversário 
Pass - passar a bola para o companheiro de equipe 
Shoot - chutar a bola em direção ao gol 
Move - mover-se 
NoAction - nenhuma ação 

Basicamente, a classe possui métodos get e set para armazenar informações como número do jogador, categoria da ação, ponto final da ação, etc.

A classe também possui uma struct simples e um método para comparar distâncias entre dois pontos. 

```cpp 
DistCompare( const rcsc::Vector2D & pos )
            : pos_( pos )
          { }

        bool operator()( const Ptr & lhs,
                         const Ptr & rhs ) const
          {
              return lhs->targetPoint().dist2( pos_ ) < rhs->targetPoint().dist2( pos_ );
          }
```

Operador () sobrecarregado para passar dois parâmetros shared_ptr do tipo da própria classe CooperativeAction.
Esse função é usada para comparar duas instâncias da classe CooperativeAction e determinar qual é o maior ou menor valor das distâncias euclidianas entre o vector2D targetPoint (ponto final da ação) e o ponto passado como parâmetro no método-construtor DistCompare da struct de mesmo nome. (**Veja:** dist2 em [Vector2D](https://bitbucket.org/herinson/ibots2d/wiki/Vector2D))
