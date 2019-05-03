# ActionStatePair

Holds two types of data: CooperativeAction e PredictState.

This class has basic get methods:

```cpp
// Returns the action
const CooperativeAction & action() const   

// Returns the predicted state
const PredictState & state() const         

// Returns the action pointer
const boost::shared_ptr< const CooperativeAction > & actionPtr() const  

// Returns the state pointer
const boost::shared_ptr< const PredictState > & statePtr() const         
```
