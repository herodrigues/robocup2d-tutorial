 

### SampleTrainer class

Like the coach (sample_coach) and the player (sample_player) there is a sample_trainer class. Basically, this class loads the 11 players and the coach team. However, you may allow the players to do nothing or simply execute specific tasks which go in the actionImpl method.

The SampleTrainer class extends the TrainerAgent class and it is recommended that you go through the librcsc source code and look at trainer_agent.cpp and trainer_agent.h files. Methods are documented and they are easy to understand by only analysing their source code. Some interesting methods of this class are:

```cpp
bool doMoveBall( const Vector2D & pos, const Vector2D & vel )
bool doMovePlayer( const std::string & teamname, const int unum, const Vector2D & pos )
bool doRecover()
bool doChangeMode( const PlayMode mode )
bool doChangePlayerType( const std::string & teamname, const int unum, const int type )
```

Open the file sample_trainer.cpp e find the actionImpl method. It is something like this:

```cpp
void
SampleTrainer::actionImpl()
{
    [...]
    //////////////////////////////////////////////////////////////////
    // Add your code here.

    //sampleAction();
    //recoverForever();
    //doSubstitute();
    //doKeepaway();
}
```

- sampleAction(): if a player is controlling the ball (if it is in the kickable area), then the trainer will put the ball in the field centre dropping it with a random speed.
- recoverForever(): calls doRecover() every 50 cycles (recovers players' stamina).
- doSubstitute(): changes players type. (To see players type, press Ctrl+H in the monitor during a match).

If you wish to use these methods, just uncomment the lines. The first method is not useful if you wish to train your team in specific game situations. This method is suitable when a desired game state is executed and you want to execute it again.
Even if you want to call sampleAction(), open its implementation and change the variable value s_state from 0 to 1 (if you do not do this then the trainer will not do anything except for starting a player which is in its kickable area).
The method implementation consists of a finite-state machine which uses a switch and the variable s_state to store the currente state.

### Configuring the trainer

Go to the team scr directory and open the file train.sh.

- Formation

Locate this line:
```bash
config_dir="${DIR}/formations-train"
```

By doing this, you will be using your own formations. If you do not know how to create and edit formations, read the tutorial [Creating formations with fedit](https://github.com/RoboCup2D/tutorial/blob/master/sections/formations-with-fedit.md).
Obviously, you can use the formations in the folder formations-dt. However, as the goal here is to use your own strategy, it is recommend that you create your formations.

Locate this line:
```bash
trainer="${DIR}/helios_trainer"
```
Put the desired trainer executable name of your team.

- Players

The following code loads the player and the trainer. The original code loads a single player:
```bash
OPT="-h ${host} -t ${teamname}"
OPT="${OPT} --player-config ${config} --config_dir ${config_dir}"
OPT="${OPT} ${debugopt}"

#if [ $number -gt 0 ]; then
#  $player ${OPT} -g &
#  $sleepprog $goaliesleep
#fi

#for (( i=2; i<=${number}; i=$i+1 )) ; do
  $player ${OPT} -n 11 &
  $sleepprog $sleeptime
#done

#if [ "${usecoach}" = "true" ]; then
#  $coach -h $host -t $teamname &
#fi

$trainer -h $host -t $teamname &
```
Replace the lines above with the following lines:

```bash
opt="--player-config ${config} --config_dir ${config_dir}"
opt="${opt} -h ${host} -p ${port} -t ${teamname}"
opt="${opt} ${fullstateopt}"
opt="${opt} --debug_server_host ${debug_server_host}"
opt="${opt} --debug_server_port ${debug_server_port}"
opt="${opt} ${offline_logging}"
opt="${opt} ${debugopt}"

ping -c 1 $host

# Loads the goalkeeper
if [ $number -gt 0 ]; then
  offline_number=""
  if  [ X"${offline_mode}" != X'' ]; then
    offline_number="--offline_client_number 1"
    if [ $unum -eq 0 ]; then
      $player ${opt} -g ${offline_number} &
      $sleepprog $goaliesleep
    elif [ $unum -eq 1 ]; then
      $player ${opt} -g ${offline_number} &
      $sleepprog $goaliesleep
    fi
  else
    $player ${opt} -g &
    $sleepprog $goaliesleep
  fi
fi

# Loads the number - 1 players 
i=2
while [ $i -le ${number} ] ; do
  offline_number=""
  if  [ X"${offline_mode}" != X'' ]; then
    offline_number="--offline_client_number ${i}"
    if [ $unum -eq 0 ]; then
      $player ${opt} ${offline_number} &
      $sleepprog $sleeptime
    elif [ $unum -eq $i ]; then
      $player ${opt} ${offline_number} &
      $sleepprog $sleeptime
    fi
  else
    $player ${opt} &
    $sleepprog $sleeptime
  fi

  i=`expr $i + 1`
done

# Loads the coach
if [ "${usecoach}" = "true" ]; then
  coachopt="--coach-config ${coach_conf}"
  coachopt="${coachopt} -h ${host} -p ${coach_port} -t ${teamname}"
  coachopt="${coachopt} ${team_graphic}"
  coachopt="${coachopt} --debug_server_host ${debug_server_host}"
  coachopt="${coachopt} --debug_server_port ${debug_server_port}"
  coachopt="${coachopt} ${offline_logging}"
  coachopt="${coachopt} ${debugopt}"


  if  [ X"${offline_mode}" != X'' ]; then
    offline_mode="--offline_client_mode"
    if [ $unum -eq 0 ]; then
      $coach ${coachopt} ${offline_mode} &
    elif [ $unum -eq 12 ]; then
      $coach ${coachopt} ${offline_mode} &
    fi
  else
    $coach ${coachopt} &
  fi
fi

$trainer -h $host -t $teamname &
```
If you do not want to load the goalkeeper, comment the lines above related to it and change the variable i before the players loading for i=1.
You can load many players as you want just changing the value of the variable number.

### Executing the trainer

Before executing the trainer, you must run the server in coach mode (you can also disable the offside rule):

```bash
$ rcssserver server::coach_w_referee=on server::use_offside=false
```

To know more about server options:
```bash
$ rcssserver server::help
```

Run the monitor:
```bash
$ rcssmonitor &
```
or
```bash
$ soccerwindow2 & 
```
Now, run the train.sh file that you had modified.
```bash
$ ./train.sh
```
**You do not need to run the sample_trainer as this is already done in the script train.sh**

You may also specify some custom options:
```bash
$ ./train.sh --help
Usage: ./train.sh [options]
  -h, --host HOST           specifies server host
  -t, --teamname TEAMNAME   specifies team name
```
The default host is localhost and the team name is HELIOS_base. It is possible to change this by using:
```bash
$ ./train.sh -t Barcelona
```
To add anoher team on the field, run the script start.sh in the opponent team scr directory.
```bash
$ ./start.sh -t opponent_team_name
```

Now you can train in your team against another team to test specific situations!
