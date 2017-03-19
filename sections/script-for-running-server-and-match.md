Create a .sh file in the folder of your preference and insert the following lines:
```bash
#!/bin/bash

rcssserver server::auto_mode=on &  # automatically start the game

cd ${DIR_OUR}
make        
./start.sh # ou ./start.sh -n x  where x is the number of players you want to load

cd ${DIR_OPP}
./start.sh # ou ./start.sh -n x  onde x é o número de jogadores que você deseja carregar

soccerwindow2 --hide-view-area --hide-stamina # or rcssmonitor

set -e
function stop_server {   
    pkill rcssserver
}

trap stop_server EXIT
```

Save this file and execute this command:
```bash
$ chmod a+x your_script.sh
```

Now, you just need to run:
```bash
$ ./script.sh /path/to/the/src/folder/of/your/team /path/to/the/src/folder/of/the/opponent/team
```

By doing that, when you stop your script with Ctrl+C in a terminal, the rcssserver will be automatically killed
