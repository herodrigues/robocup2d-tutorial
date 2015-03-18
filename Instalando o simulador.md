  Os passos a seguir foram feitos e testados utilizando a versão 12.04 LTS da distribuição Ubuntu Linux

### Configurando o ambiente e instalando o servidor e monitor

Abra o terminal (CTRL+ALT+T) e execute os seguintes comandos:

```bash
$ sudo apt-add-repository ppa:gnurubuntu/rubuntu
$ sudo apt-get update
$ sudo apt-get install g++
$ sudo apt-get install build-essential
$ sudo apt-get install libboost-all-dev
$ sudo apt-get install qt4-dev-tools
$ sudo apt-get install rcssserver
$ sudo apt-get install rcssmonitor
```

Agora, vá até o repositório oficial da Robocup no SourceForge clicando [aqui](http://en.sourceforge.jp/projects/rctools/releases/).

Faça os downloads dos seguintes arquivos:
- librcsc
- agent2d

Atualmente, estamos utilizando as seguintes versões: [agent2d-3.1.1](http://en.sourceforge.jp/projects/rctools/downloads/55186/agent2d-3.1.1.tar.gz/) e [librcsc-4.1.1](http://en.sourceforge.jp/projects/rctools/downloads/51941/librcsc-4.1.0.tar.gz/). Vá até o diretório onde você salvou os arquivos e siga as instruções (faça na ordem):  _Note que x.x.x é a versão do arquivo baixado._

Abra um terminal e descompacte os arquivos com seguintes comandos:

```bash
$ tar -zxpf librcsc-x.x.x.tar.gz
$ tar -zxpf agent2d-x.x.x.tar.gz
```

**NOTA**: todas as pastas do diretório no qual você está salvando os arquivos da librcsc, não devem conter espaços em seus nomes.


### Instalando a librcsc


**IMPORTANTE:** _As informações de todos os jogadores são passadas para um log, onde é usado o separador decimal ponto(.). Como no Brasil o separador decimal é a vírgula, acontece um erro de leitura. Esse erro foi solucionado graças ao Gilberto Alves Santos da equipe Petsoccer. 
 É aconselhável que a instalação da sua distribuição Linux esteja em inglês. Se ela não estiver, execute o comando `export LC_NUMERIC="C"` no terminal para que o erro citado acima não ocorra._
 
Entre na pasta do arquivo descompactado:

```bash 
$ cd librcsc-x.x.x/
```

Entre com os comandos abaixo:

**Nota:** _Se tiver problemas de permissão no primeiro comando, ao invés de_ `./configure` _execute_ `sh ./configure`.

```bash 
$ ./configure
$ make
$ sudo make install
```

### Instalando o agent2d

Entre no diretório do arquivo descompactado:

```bash 
$ cd agent2d-x.x.x/
```

Entre com os comandos abaixo:

```bash 
$ ./configure
$ make
$ sudo make install
```

### (Opcional) Instalando o monitor soccerwindow2

Existe outro monitor da Robocup com mais detalhes da partida e informações do jogador.  Este monitor é usado na competição mundial da Robocup. Se deseja instalá-lo, basta seguir estas instruções:

No repositório da Robocup citado no início deste tutorial, baixe o arquivo soccerwindow2. Ou clique [aqui](http://en.sourceforge.jp/projects/rctools/downloads/51942/soccerwindow2-5.1.0.tar.gz/) para baixar a última versão utilizada por nossa equipe.

Abra um terminal e descompacte o arquivo:

```bash 
$ tar -zxpf soccerwindow2-x.x.x.tar.gz
```

Entre no diretório do arquivo descompactado:

```bash
$ cd soccerwindow2-x.x.x.tar.gz
```

Entre com os seguintes comandos:

```bash 
$ ./configure
$ make
$ sudo make install
```

Provavelmente, os seguintes erros serão mostrados após:

```bash
/usr/bin/ld: cannot find -laudio
/usr/bin/ld: cannot find -lpng
/usr/bin/ld: cannot find -lgobject-2.0
/usr/bin/ld: cannot find -lXi
/usr/bin/ld: cannot find -lXrender
/usr/bin/ld: cannot find -lfreetype
/usr/bin/ld: cannot find -lfontconfig
```
Para isso, basta rodar os seguintes comandos:

```bash
$ sudo apt-get install libaudio-dev
$ sudo apt-get install libgtk-3-dev
```

### Finalizando

Com tudo instalado, está na hora de colocar uma partida para rodar e testar se tudo ocorreu sem problemas. Para isso, clique [aqui](https://bitbucket.org/herodrigues/ibots2d/wiki/Rodando-uma-partida-com-o-agent2d) e siga o tutorial.