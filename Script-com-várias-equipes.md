Binários no site oficial da RoboCup: www.socsim.robocup.org/files/2D/binary

Não esqueça de editar os nomes das pastas!

Crie um arquivo run.sh em cada pasta dos binários exatamente no mesmo diretório do arquivo start
```bash
#!/bin/bash

for i in {1..11}
do
    ./start localhost . $i &
    sleep 1
done
```

Crie um arquivo .sh com o conteúdo abaixo:

```bash
#!/bin/bash

rcssserver server::log_times=on & 

# iBots2D
cd $TEAMS_DIR/ibots2d/src
make        
./start.sh --debug --debug-server-connect --log-dir .

TEAMS_DIR=$1

# Agent2D
#cd $TEAMS_DIR/agent2d-3.1.1/src
#./start.sh 

# Axiom2012
#cd $TEAMS_DIR/axiom2012
#./run.sh

# Axiom2013
#cd $TEAMS_DIR/axiom2013
#./run.sh 

# Borregos2012
#cd $TEAMS_DIR/borregos2012
#./run.sh

# FCPerspolis2013
#cd $TEAMS_DIR/fcperspolis2013
#./run.sh 

# FCPortugal2012
#cd $TEAMS_DIR/fcportugal2012
#./run.sh

# GDUT_Tiji2012
#cd $TEAMS_DIR/gdut_tiji2012
#./run.sh

# GDUT_Tiji2013
#cd $TEAMS_DIR/gdut_tiji2013
#./run.sh

# Gliders2012
#cd $TEAMS_DIR/gliders2012
#./run.sh

# GPR2D_2012
#cd $TEAMS_DIR/gpr2d2012
#./run.sh

# GPR2D_2013
#cd $TEAMS_DIR/gpr2d2013
#./run.sh

# HfutEngine2013
#cd $TEAMS_DIR/hfutengine2013
#./run.sh

# HELIOS2012
#cd $TEAMS_DIR/helios2012
#./start.sh

# ITAndroids2012
#cd $TEAMS_DIR/itandroids2012
#./run.sh

# LegenDary2013
#cd $TEAMS_DIR/legendary2013
#./run.sh

# MarliK2011
#cd $TEAMS_DIR/marlik2011/src
#./start.sh

# MarliK2012
#cd $TEAMS_DIR/marlik2012
#./run.sh

# Nadco2012
#cd $TEAMS_DIR/nadco2012
#./run.sh

# Riton2012
#cd $TEAMS_DIR/riton2012
#./run.sh

# YuShan2012
#cd $TEAMS_DIR/yushan2012
#./run.sh

# YuShan2013
#cd $TEAMS_DIR/yushan2013
#./run.sh

soccerwindow2 --hide-view-area --hide-stamina --maximize

set -e
function stop_server {   
    pkill rcssserver
}

trap stop_server EXIT
```

Dê permissão de execução:
```bash
$ chmod a+x nome_do_arquivo.sh
```

Agora, descomente a linha da equipe adversária que deseja executar e, em seguida, execute a partida com o seguinte comando:

```bash
$ ./nome_do_arquivo.sh /diretorio/dos/binarios/das/equipes
```