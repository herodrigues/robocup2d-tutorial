To do this tutorial, you must had read the [previous tutorial](https://github.com/robocup2d/robocup2d/wiki/Instalando-the-soccer-simulator).

### Running the server and monitor

Open a terminal and run the server:

```bash
$ rcssserver &
```

Now we need a monitor to visualize the match. If you have installed rcssmonitor and soccerwindow2, choose one and run it:

```bash
$ rcssmonitor &
```
or
```bash
$ soccerwindow2 &
```

### Take teams on the field

Go to the agent2d directory and run:

```bash
$ cd src/
$ ./start.sh -t team_name
```

_Nota: replace **team_name** with the desired team name.
If you have permission problems with the second command, run_ `sudo chmod +x start.sh`.
_If you still have problems, edit the folder permissions by executing_ `sudo chmod 777 *`.

Open another terminal and run the same command cited above just placing a different team name.

### Conclusion

Now you have two teams on the field. Just use Ctrl+K to perform a match kick-off.
