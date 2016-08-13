### Configurando o ambiente e instalando o server

Os passos a seguir foram testados e executados utilizando Ubuntu 12.04 LST e Debian Wheezy 7

Abra um terminal e execute:

```bash
$ sudo apt-get install g++ build-essential libboost-all-dev qt4-dev-tools libaudio-dev libgtk-3-dev libxt-dev
```

**UBUNTU**

```bash
$ sudo apt-add-repository ppa:gnurubuntu/rubuntu
$ sudo apt-get update
```
Isto adicionará automaticamente uma entrada no source list baseada na versão do Ubuntu que você está utilizando.

Instale o server:
```bash
$ sudo apt-get install rcssserver
```

**OUTRAS DISTRIBUIÇÕES LINUX**

_Problemas podem ocorrer em versões mais novas de distribuições Linux que utilizam versões da library bison superior à 2.7, portanto, é recomendável instalar a versão 2.7.1: http://askubuntu.com/questions/444982/install-bison-2-7-in-ubuntu-14-04_

Instale as libs bison e flex:
```bash
$ sudo apt-get install bison flex
```

Faça o download do arquivo rcssserver [aqui](http://sourceforge.net/projects/sserver/files/).

_Observe que x.x.x é a versão do arquivo.
No Debian 8, especifique o caminho da boost ```$ ./configure --with-boost-libdir=/usr/lib/x86_64-linux-gnu```_

```bash
$ tar -zxpf rcssserver-x.x.x.tar.gz
$ cd rcssserver-x.x.x
$ ./configure && make   
$ sudo make install
```
____________________________________________________________________________________

Os passos a seguir independem da sua distribuição linux.

Agora, vá até o repositório oficial da Robocup no SourceForge clicando [aqui](http://en.sourceforge.jp/projects/rctools/releases/).

Faça os downloads dos seguintes arquivos:
- librcsc
- agent2d

Atualmente, estamos utilizando as seguintes versões: [agent2d-3.1.1](http://en.sourceforge.jp/projects/rctools/downloads/55186/agent2d-3.1.1.tar.gz/) e [librcsc-4.1.1](http://en.sourceforge.jp/projects/rctools/downloads/51941/librcsc-4.1.0.tar.gz/). Vá até o diretório onde você salvou os arquivos e siga as instruções (faça na ordem):  _Observe que x.x.x é a versão do arquivo baixado._

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

### Instalando o monitor

Existem dois monitores: rcssmonitor e soccerwindow2

Eu recomendo usar o soccerwindow2 por ser um monitor bem mais completo e que também pode ser usado como debugger. Mais informações em [SoccerWindow2 como debugger](https://github.com/robocup2d/wiki/wiki/Soccerwindow2-como-debugger).

**Instalando o rcssmonitor**

Se você está usando Ubuntu, basta executar:
```bash
$ sudo apt-get install rcssmonitor
```

Se está usando outra distribuição Linux, faça o download do rcssmonitor [aqui](http://sourceforge.net/projects/sserver/files/rcssmonitor/15.1.1/rcssmonitor-15.1.1.tar.gz/download).

Após ter feito o download, abra um terminal e execute os comandos:

```bash 
$ tar -zxpf rcssmonitor-x.x.x.tar.gz
$ cd rcssmonitor-x.x.x.tar.gz
$ ./configure
$ make
$ sudo make install
```

**Instalando o SoccerWindow2**

Faça o download do soccerwindow2 [aqui](http://en.sourceforge.jp/projects/rctools/downloads/51942/soccerwindow2-5.1.0.tar.gz/).

Abra um terminal e execute:
```bash 
$ tar -zxpf soccerwindow2-x.x.x.tar.gz
$ cd soccerwindow2-x.x.x.tar.gz
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
```

### Finalizando

Com tudo instalado, está na hora de colocar uma partida para rodar e testar se tudo ocorreu sem problemas. Para isso, clique [aqui](https://github.com/robocup2d/robocup2d/wiki/Rodando-uma-partida-com-o-agent2d) e siga o tutorial.
