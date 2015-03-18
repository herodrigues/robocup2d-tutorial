Autotools é um conjunto de ferramentas de programação para auxiliar na compilação de pacotes de código-fonte portáveis para sistemas Unix-like. 
https://developer.gnome.org/anjuta-build-tutorial/stable/create-autotools.html.en

Esse ferramenta vai ser de extrema importância pois é muito trabalhoso ficar editando o Makefile do agent2D manualmente.

Antes de tudo, instale o Autotools:
```bash
$ sudo apt-get install autotools-dev
```

Agora, entre na pasta do código-fonte do ibots2D e execute o comando:
```bash
$ autoreconf
```
O comando acima só é necessário pois o Makefile original do agent2D foi feito com uma versão mais antiga do Autotools.

Na pasta src do código-fonte do ibots2D existe um aquivo chamado Makefile.am. É esse arquivo que você adicionará as suas classes. Após isso, vá um nível acima da pasta src e execute.

```bash
$ automake
$ ./configure
```
O primeiro comando gera o arquivo Makefile.in a partir do Makefile.am. O segundo comando transforma o Makefile.in em Makefile.
Você adicionará suas classes no arquivo Makefile.am como nesse exemplo:
```bash
## Process this file with automake to produce Makefile.in

PLAYERSOURCES = \
        sua_nova_classe_aqui.cpp \
	body_advance_ball_test.cpp \
	body_clear_ball2008.cpp \
        # ....
PLAYERHEADERS = \
        sua_nova_classe_aqui.h \
	body_advance_ball_test.h \
	body_clear_ball2008.h \
        # ...
```
Feito isso, agora é só ir até a pasta src novamente e compilar o projeto com o comando:
```bash
$ make
```
