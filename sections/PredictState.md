# PredictState

Predict some game variables in a specific match state using a player's world model.

Some of these variables are:
- everything related to the ball (rcsc::ballObject)
- match time (rcsc::GameTime)
- game mode (rcsc::GameMode)
- field side ID (rcsc::SideID)

Some important methods:

```cpp
// check which player has the ball, either teammate or opponent, and returns the player's pointer reference
const rcsc::AbstractPlayerObject * ballHolder() const

// check if the current player is not the same that has the ball
const rcsc::AbstractPlayerObject & self() const        
```
