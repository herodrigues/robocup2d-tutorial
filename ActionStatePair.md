Armazena dois tipos de dados: CooperativeAction e PredictState. 

Possui métodos get básicos e auto-explicáveis pelo nome como:

```cpp
const CooperativeAction & action() const   // Retorna a ação
const PredictState & state() const         // Retorna o estado previsto
const boost::shared_ptr< const CooperativeAction > & actionPtr() const    // retorna o ponteiro da ação
const boost::shared_ptr< const PredictState > & statePtr() const          // retorna o ponteiro do estado
```