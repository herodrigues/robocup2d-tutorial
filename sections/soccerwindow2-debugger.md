**Tutorial anterior: [Rodando uma partida com o agent2D](https://github.com/RoboCup2D/tutorial/blob/master/sections/running-a-match-with-agent2d.md)**

O SoccerWindow2 é um poderoso monitor que pode ser usado como debugger inclusive com a partida rodando.

Abra um terminal e inicie o SoccerWindow2:
```bash
$ soccerwindow2 &
```

_Se não deseja executar o soccerwindow pelo terminal, você pode adicioná-lo no menu de aplicações da sua distribuição Linux. Leia sobre isso [aqui](https://developer.gnome.org/integration-guide/stable/desktop-files.html.en)_


No menu, abra _Monitor > Launcher_ Dialog ou simplesmente Ctrl+X:

Coloque o caminho para o script start.sh (fica na pasta src) dos dois times seguido dos argumentos _--debug --debug-connect-server --log-dir DIRECTORY_, onde DIRECTORY é a pasta onde você deseja salvar os logs de debug. Se deseja visualizar informações das duas equipes, coloque os argumentos de debug nas duas.

As equipes entrarão em campo e o servidor será iniciado. 
A informação de debug ainda não aparece, pois é necessário escolher em qual membro ou membros das equipes você desejar manter o foco.

No menu, vá em _Debug > View Preference_ ou simplesmente Ctrl+V. Na aba _Object_, vá na seção _Player Selection_ e escolha entre os seguintes items:
- **Auto left**: visualiza informações de todos os jogadores do time que está do lado esquerdo do campo
- **Left number X**: visualiza informações do jogador número X do time que está do lado esquerdo do campo 
- **Left coach**: visualiza informações do técnico do time que está do lado esquerdo do campo 
- **Auto right**: visualiza informações de todos os jogadores do time que está do lado direito do campo
- **Right number X**: visualiza informações do jogador número X do time que está do lado direito do campo 
- **Right coach**: visualiza informações do técnico do time que está do lado direito do campo 

Pressione Ctrl+K para iniciar a partida.
_Obs: como o rcssserver não foi iniciado em auto_mode=on, será preciso dar Kick off na partida novamente após 3000 ciclos (meio-tempo da partida)._

A imagem abaixo mostra uma partida em pausa no ciclo 2810 com o debug ativo para toda a equipe iBots2D:

![](https://github.com/RoboCup2D/tutorial/raw/master/images/debug-view.png)
> Imagem maior [aqui](https://github.com/RoboCup2D/tutorial/raw/master/images/debug-view.png)


- Os círculos azuis representam as últimas posições conhecidas dos adversários pelo jogador número 7 (jogador que está com a bola).
- Os círculos verdes representam as últimas posições conhecidas dos companheiros de equipe pelo jogador número 7 (jogador que está com a bola).
- O círculo laranja com um x no centro, representa a posição onde o jogador 7 desejou passar a bola.
- A linha vermelha pontilhada representa a possível trajetória da bola
- A linha preta do jogador 6 para o 7, indica que o jogador 7 recebeu a mensagem enviada pelo jogador 6.
- No canto superior esquerdo logo abaixo do nome da equipe Helios_base, são escritas informações de comunicação dos jogadores. Neste caso, o jogador sete tem 3 ações a serem tomadas: mover-se (BasicMove78), girar o pescoço para fazer um scan (NeckScan) e não atacar (AttOff).

Todas essas informações podem ser selecionadas no menu em _Debug > Debug Message_.

Para ver o debug em tempo real da partida, basta ir em _File > Open debug view_ e selecionar o diretório que você passou como paramêtro em _--log-dir_.

É possível também visualizar o log de um replay de uma partida. Para isso, abra o rcg da partida desejada e logo depois abra o diretório onde você salvou o debug view.
