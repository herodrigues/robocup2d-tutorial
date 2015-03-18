O objetivo dessa classe é prever algumas variáveis do jogo em um estado específico de acordo com o modelo de mundo de um jogador.

Por exemplo:
- tudo relativo à bola (rcsc::ballObject)
- tempo do jogo (rcsc::GameTime)
- modo do jogo (rcsc::GameMode)
- lado do campo (rcsc::SideID)

Alguns métodos importantes:

```cpp
const rcsc::AbstractPlayerObject * ballHolder() const  // verifica quem está com a bola, adversário ou
                                                       // companheiro, e retorna a referência do jogador
const rcsc::AbstractPlayerObject & self() const        // verifica se o jogador a ser interagido não é o
                                                       // mesmo que está com a bola
```

