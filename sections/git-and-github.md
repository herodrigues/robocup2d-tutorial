Não vou entrar em detalhes sobre instalação do git aqui. Para isso, separei dois excelentes links:

Um tutorial bem simples em português sobre instalação e configuração do git:<br>
http://rogerdudler.github.io/git-guide/index.pt_BR.html

E é claro, a própria documentação do git:<br>
http://git-scm.com/docs/gittutorial

O foco desse tutorial é entender como os branches funcionam e como eles vão ser utilizados no projeto do ibots2D.

Primeiro, um branch nada mais é que uma ramificação do projeto principal. O projeto princial, por sua vez, chamado de master é o código-fonte que foi 'upado' pela primeira vez no Github.

A ideia aqui é fazer do código puro do agent2D o master do projeto. Assim, cria-se um branch para cada novo behaviour ou classe e, só é feito o merge com o master, se essa nova funcionalidade estiver funcionando 100%.

Claro que para testar os behaviours é necessário modificar as classes Roles e isso gerará conflito ao fazer merge com o master. Portanto, antes de fazer o merge, é necessário fazer com que o código das Roles fique igual ao do master.
Com uma nova funcionalidade testada e devidamente debuggada, ela já pode ir para o master.
