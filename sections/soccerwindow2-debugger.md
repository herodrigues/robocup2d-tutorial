# SoccerWindow2

SoccerWindow2 is a powerful monitor that can be used as a debugger even with a running match.

Open a terminal and run:
```bash
$ soccerwindow2 &
```

In the main menu, click on  _Monitor > Launcher_ Dialog or press Ctrl+X:

Set the path to the `start.sh` script (located in the src folder) for both teams with the arguments _--debug --debug-server-connect_.

The teams will appear in the field and the server will be started. The debug information shows up immediately on the screen. If needed, you can choose on which player you want to focus. 

Go to _Debug > View Preference_ or press Ctrl+V. In the _Object_ tab, navigate to the section _Player Selection_ and choose one of the following items:
- **Auto left**: visualize information of all players of the left team (left side of the field)
- **Left number X**: visualize information of a specific player t of the left team (left side of field).
- **Left coach**: visualize information of the left team coach (left side of field).
- **Auto right**: visualize information of all players of the right team (right side of the field)
- **Right number X**: visualize information of a specific player t of the right team (right side of field).
- **Right coach**: visualize information of the right team coach (right side of field).

The image below showsa match paused at cycle 2810 with the debugger active for all players of the iBots2D team:

![](https://github.com/RoboCup2D/tutorial/raw/master/images/debug-view.png)
> Bigger image [here](https://github.com/RoboCup2D/tutorial/raw/master/images/debug-view.png)

- The blue circles represent the last known positions of the opponents viewed by the player number 7 (player with the ball possession).
- The green circles represent the last known positions of the teammates viewed by the player number 7 (player with the ball possession).
- The orange circle with a X on its center represents the position where the player number 7 tried to pass the ball.
- The tracing red line represents the probable ball path.
- The black line from the player number 6 to the player number 7 indicates that the player 7 received a message sent by the player 6.
- On the left top corner right below the Helios_base team name, information about players communications are written. In this example, the player 7 has three actions to be taken: move (BasicMove78), turn its neck to scan the field (NeckScan) and do not attack (AttOff).

All this information can be selected using the main menu at _Debug > Debug Message_.

TO view the debug information of a match replay, you need to add the flag _--log-dir DIRECTORY_ in the start.sh script of your team and also add the flags _--debug --debug-server-connect_ (where DIRECTORY is the folder where you want to save the match logs) é o diretório onde você deseja salvar os logs). When the match is over, you only need to open the match RCG file and the log files using the File menu.
