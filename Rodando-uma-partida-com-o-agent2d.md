  Para realizar as instruções descritas neste tutorial, siga o tutorial anterior sobre a [Instalação do simulador](https://bitbucket.org/herodrigues/iBots/wiki/Instalando-o-simulador).

### Rodando o servidor e o monitor

Abra um terminal (CTRL+ALT+T) e digite o comando:

```bash
$ rcssserver &
```

Com isso, o servidor já está rodando. 
Agora precisamos rodar um monitor para visualizar a partida que será iniciada posteriormente. 
Se você instalou os dois monitores, rcssmonitor e soccerwindow2, escolha qual deseja rodar. Para isso, entre com o comando:

```bash
$ rcssmonitor &
```
ou
```bash
$ soccerwindow2 &
```

### Colocando as equipes em campo

Com o monitor rodando, precisamos agora por as equipes em campo.
Vá até o diretório onde você extraiu o agent2d e entre com os comandos:

```bash
$ cd src/
$ ./start.sh -t nomeDaEquipe
```

_Nota: substitua **nomeDaEquipe** pelo nome que deseja que a equipe possua.
Se tiver problemas de permissão no segundo comando, execute_ `sudo chmod +x start.sh`.
_Se os problemas persistirem, dê premissão para a pasta toda executando_ `sudo chmod 777 *`.

Uma equipe já está em campo. É necessário por outra equipe em campo (jura?!).
Abra outro terminal e entre com o mesmo comando citado acima, alterando o nome da equipe.

### Finalizando

Com tudo feito, você terá os dois times em campo prontos para o jogo. Agora, basta dar um Ctrl+K para começar a partida.