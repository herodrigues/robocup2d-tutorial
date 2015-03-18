Iniciando pela classe de onde herdam mais classes: ActionGenerator.
Essa classe gera uma cadeia de ações para serem decididas pelo agente.

Segue a figura que mostra a herança de classes.

<figura>

Essa classe possui dois membros públicos: um "ponteiro compartilhado" e um "ponteiro constante compartilhado".

"The shared_ptr class template stores a pointer to a dynamically allocated object, typically with a C++ new-expression. The object pointed to is guaranteed to be deleted when the last shared_ptr pointing to it is destroyed or reset"
 **Mais em**: http://www.boost.org/doc/libs/1_53_0/libs/smart_ptr/shared_ptr.htm

A classe também possui mais um construtor e um construtor-cópia não utilizados de acordo com o comentário escrito acima deles.

Segue alguns métodos dessa classe:
```cpp
/*!
  \brief Gera uma cadeia de pares "ação-estado" (ActionStatePair)
  \param result Armazena o valor gerado pelo par "ação-estado"
  \param state Último estado a gerar uma nova "ação-estado"
  \param wm Visão de mundo atual no estado inicial
  \param path Cadeia de "ação-estado" do estado inicial até o estado final
*/
virtual void generate( std::vector< ActionStatePair > * result,
                   const PredictState & state,
                   const rcsc::WorldModel & wm,
                   const std::vector< ActionStatePair > & path ) const = 0;

/*!
* \brief Adiciona os estados gerados ao vector M_generators 
* \param g Instância da classe ActionGenerator
*/
void addGenerator( const ActionGenerator * g )
      {
          if ( g )
          {
              M_generators.push_back( ConstPtr( g ) );
          }
      }
```

Essa classe serve de herança para diversas classes que gerarão cadeias de ações básicas como chutar, passar e cruzar. Todas essas ações são levadas em conta de acordo com a ação a ser tomada em grupo (CooperativeAction) e com o estado a ser previsto (PredictState). Essas duas informações são armazenadas numa instância da classe ActionStatePair.

Todas as classes do tipo "action_gen_" possuem um método generate (que é um método na classe pai, ActionGenerator). O método generate tem por objetivo gerar uma cadeia de ações a serem tomadas de acordo com cada estado previsto. O modelo de mundo do jogador é passado como parâmetro, assim como um ponteiro para vector que armazenará o resultado de ActionStatePair.

Cada método generate de cada classe act_gen_, consequentemente, tem sua particularidade e estão explicados no seu específico wiki.


