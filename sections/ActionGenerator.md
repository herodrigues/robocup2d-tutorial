# ActionStateGenerator

Starting from the class which extends more classes: ActionGenerator.
This class generates a chain of actions to be taken by the agent.

The class inheritance is shown in the picture below:

<picture>

This class has two public members: a shared pointer and a constant shared pointer.

"The shared_ptr class template stores a pointer to a dynamically allocated object, typically with a C++ new-expression. The object pointed to is guaranteed to be deleted when the last shared_ptr pointing to it is destroyed or reset"
 **Read more**: http://www.boost.org/doc/libs/1_53_0/libs/smart_ptr/shared_ptr.htm

This class also has one more constructor a copy constructor not used as stated in the class doc strings.

Here are some of the class methods:
```cpp
/*!
  \brief Generates a chain of "action-state" pairs (ActionStatePair)
  \param result Store the value generated for the "action-state" pair
  \param state Last state to generate an "action-state"
  \param wm World model of the initial state
  \param path Chain of "action-state" of the initial state until the final state
*/
virtual void generate( std::vector< ActionStatePair > * result,
                   const PredictState & state,
                   const rcsc::WorldModel & wm,
                   const std::vector< ActionStatePair > & path ) const = 0;

/*!
* \brief Add generated states to the vector M_generators
* \param g ActionGenerator instance
*/
void addGenerator( const ActionGenerator * g )
      {
          if ( g )
          {
              M_generators.push_back( ConstPtr( g ) );
          }
      }
```

This class is the base class for several other classes that generate chains of basic actions such as kick, pass and cross. All of these actions are taken into account according to the action that is executed for more than one agent (CooperativeAction) and the predicted state (PredictState). This information is stored in a ActionStatePair instance.

All "action_gen_" type classes have a generate method (a method of the base class, ActionGenerator). The generate method creates a chain of actions that will be executed according to the predicted state. The player's world model is used as parameter and also a pointer to the vector that will store the result of ActionStatePair.
