 

### Sobre a classe SampleTrainer

Assim como o técnico (sample_coach) e o jogador (sample_player) há um sample_trainer. Basicamente, esta classe roda os 11 jogadores e o técnico da sua equipe. Porém, você pode permitir que os jogadores façam nada ou executem apenas o que for passado no método actionImpl da classe SampleTrainer.

A classe SampleTrainer extende da classe TrainerAgent, recomendo que você olhe nos fontes da librcsc e procure os arquivos trainer_agent.cpp e trainer_agent.h. Os métodos estão documentados e são fáceis de entender apenas lendo o código. Alguns métodos interessantes que podemos citar dessa classe são:

```cpp
bool doMoveBall( const Vector2D & pos, const Vector2D & vel )
bool doMovePlayer( const std::string & teamname, const int unum, const Vector2D & pos )
bool doRecover()
bool doChangeMode( const PlayMode mode )
bool doChangePlayerType( const std::string & teamname, const int unum, const int type )
```

Agora que você já sabe os principais métodos da classe TrainerAgent, abra o arquivo sample_trainer.cpp e localize o método actionImpl(). Você verá algo assim:

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

Sobre os métodos:
- sampleAction(): identifica se um jogador pegou a bola (está dentro da sua área chutável) e o trainer coloca a bola no centro do campo e a atira com uma velocidade aleatória.
- recoverForever(): chama o método doRecover(), frequentemente, a cada 50 ciclos (recupera a stamina dos jogadores).
- doSubstitute(): fica trocando o tipo dos jogadores. (Com uma partida rolando, no monitor, aperte Ctrl+H para ver os tipos dos jogadores).

Se quiser utilizar esses métodos, basta tirar os comentários. O primeiro método não é muito útil se você vai treinar a equipe para determinadas situações. O ideal é utilizá-lo quando um estado de jogo que você determinou tiver sido executado e você queira recomeçá-lo. 
Se mesmo assim quiser usar o sampleAction(), localize-o e troque o valor da variável static int s_state de 0 para 1 (senão o nosso treinador não fará nada a menos que iniciar com um jogador dentro da área chutável da bola).  Quanto à implementação do método, ela é feita como uma máquina de estados finitos com uso de switch e a variável s_state para guardar o estado atual. A implementação é simples de entender apenas lendo o código e os comentários. 

### Configurando o trainer

Vá até a pasta src da sua equipe e abra o arquivo train.sh.

- Formação

Localize esta linha:
```bash
config_dir="${DIR}/formations-train"
```

Com isso, você estará indicando onde estão os seus arquivos de formações. Se não souber editar formações, veja o tutorial [criando formações com o fedit](https://bitbucket.org/herodrigues/ibots2d/wiki/Criando-forma%C3%A7%C3%B5es-com-o-fedit).
Obviamente, você pode utilizar a pasta formations-dt. Mas, como o objetivo é utilizar suas próprias formações de treino, é ideal que você as faça.

Localize esta linha:
```bash
trainer="${DIR}/helios_trainer"
```
E substitua pelo nome do executável do trainer da sua equipe.

- Jogadores

As linhas a seguir efetuam o carregamento dos jogadores e do técnico. Você irá encontrar boa parte comentada. O código original carrega apenas um jogador.
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
Troque as linhas acima por estas:

```bash
opt="--player-config ${config} --config_dir ${config_dir}"
opt="${opt} -h ${host} -p ${port} -t ${teamname}"
opt="${opt} ${fullstateopt}"
opt="${opt} --debug_server_host ${debug_server_host}"
opt="${opt} --debug_server_port ${debug_server_port}"
opt="${opt} ${offline_logging}"
opt="${opt} ${debugopt}"

ping -c 1 $host

# Carrega o goleiro
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

# Carrega os outros number - 1 jogadores 
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

# Carrega o Coach 
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
Se não quiser carregar o goleiro, apague a parte correspondente a ele e altere a variável i antes do carregamento dos jogadores para i=1.
Obviamente, você pode carregar quantos jogadores quiser, basta alterar a variável number para o número que desejar.

### Executando o trainer

Antes de executar o trainer, você deve rodar o servidor em modo coach e também você pode optar por desativar o impedimento. Execute:
```bash
$ rcssserver server::coach_w_referee=on server::use_offside=false
```
Assim, seus jogadores não ficarão impedidos mesmo que só haja sua equipe em campo. 

Para saber mais opções do servidor, execute:
```bash
$ rcssserver server::help
```

Execute o monitor:
```bash
$ rcssmonitor &
```
ou
```bash
$ soccerwindow2 & 
```
Agora, basta executar o arquivo train.sh que você acabou de modificar.
```bash
$ ./train.sh
```
**Você não precisa executar o sample_trainer, pois no script train.sh isso já é feito.**

Você pode especificar alguns paramêtros também:
```bash
$ ./train.sh --help
Usage: ./train.sh [options]
  -h, --host HOST           specifies server host
  -t, --teamname TEAMNAME   specifies team name
```
Para o host o padrão é localhost e, para o teamname, o padrão é HELIOS_base. Você pode mudar o nome do time assim:
```bash
$ ./train.sh -t Barcelona
```
Se quiser adicionar outra equipe para jogar contra a sua, basta entrar no diretório dela e executar o script start.sh.
```bash
$ ./start.sh -t NomeDaEquipeAdversaria
```

Agora você já pode treinar sua equipe sem ter que rodar uma "partida normal". Até a próxima :D