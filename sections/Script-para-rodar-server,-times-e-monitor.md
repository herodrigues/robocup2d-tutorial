Crie um arquivo .sh na pasta de sua preferência e coloque o código abaixo:
```bash
#!/bin/bash

rcssserver server::auto_mode=on &  # inicia o jogo automaticamente

cd ${DIR_OUR}
make        # Compila o código caso você tenha feito alguma alteração
./start.sh # ou ./start.sh -n x  onde x é o número de jogadores que você deseja carregar

cd ${DIR_OPP}
./start.sh # ou ./start.sh -n x  onde x é o número de jogadores que você deseja carregar

soccerwindow2 --hide-view-area --hide-stamina # ou rcssmonitor

set -e
function stop_server {   
    pkill rcssserver
}

trap stop_server EXIT
```
Salve com o nome de sua preferência e depois execute em um terminal o seguinte comando:
```bash
$ chmod a+x seu_script.sh
```

Agore é só rodar o script:
```bash
$ ./seu_script.sh /caminho/para/pasta/src/da/sua/equipe/ /caminho/para/pasta/src/da/equipe/adversaria/
```
Feito isso, quando você finalizar o script com Ctrl+C no terminal, o processo rcssserver será finalizado automaticamente.