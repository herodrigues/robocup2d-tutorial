No SoccerWindow2, após o término de uma partida (ou até mesmo antes do término se você preferir) e vá em File > Save DebugView, escolha o diretório e salve.

Para visualizar esses dados, basta rodar o Soccerwindow2, abrir o .rcg da partida e logo após ir em File > Open DebugView e selecione o diretório onde você salvou os arquivos.

View Preferences > selecionar o lado que o time está.

Atenção! Existem dois logs diferentes: o log do SoccerWindow2 é utilizado a partir de uma instância do player agent, exemplo:

```
#!cpp
agent->debugClient().addMessage("Mensagem");
```

Há também o log do próprio rcssserver que pode ser acessado através da variável estática dLog.


