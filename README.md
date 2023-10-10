# Tetris
Tetris with a Q-learning and Deep Q Network. 

Original DQN

![Deep Q Network playing Tetris](Original_mode_dqn.gif)

Hold Mode DQN

![Deep Q Network playing Tetris](Hold_mode_dqn.gif)

## How it works

### Reinforcement learning
Reinforcement learning is used to determine what *action* should be taken that would maximize *reward* when given a *state*. 

#### State

| Name  | Description |
| ---: | :--- |
| Holes  | Number of empty cells covered by a full cell  |
| Landing height  | Height where the last piece is added  |
| Eroded piece cells  | (Rows cleared) × (Cells removed from the last piece) |
| Row transitions  | Number of horizontal cell transitions  |
| Column transitions  | Number of vertical cell transitions  |
| Cumulative wells  | The sum of all wells  |
| Bumpiness | A total of the difference between the height of each column  |
| Aggregate height | Sum of the heights of each column  |
| Rows cleared  | The amount of rows cleared  |

#### Reward
Rewards are based on the original Tetris game but reward is also given when the actor stays alive and taken when losing.

| Name  | Reward |
| ---: | :---: |
| Alive  | +1  |
| Clearing 1 Row  | +40  |
| Clearing 2 Rows  | +100  |
| Clearing 3 Rows  | +300  |
| Clearing 4 Rows  | +1200  |
| Game Over  | -5  |

#### Action
As mentioned before it compares all possible states to find the one that would result in the highest reward. 
The action that would result in the best board state will be chosen.
The action is just a tuple of the rotation count (0 to 3) and the column (0 to 9) that the piece should drop at. 

### Q-Learning
If Q-Learning was not used the neural network would prefer to get immediate reward rather than future rewards. 
In our case the actor would want to clear a row even if it would mean creating an obstacle which would be bothersome for the rest of the game.
That is why it is important to use Q-Learning.

### Training
At first the AI explores by selecting random actions.
Every episode it will train itself with randomly selected experiences from previous games (and also applying Q-Learning).
Slowly it will shift from mostly exploration to exploitation which means that the neural network will chose the actions.


## How to run
Run `run_human.py` if you'd like to play Tetris.

Run `run_play_pierre.py.py` if you'd like to see AI with Pierre Dellacherie algorithm.

Run `Q-learning.py` if you'd like to train Q-learning agent.

Run `run_play_dqn.py` if you'd like to see the AI play Tetris without considering "Hold" action.

Run `run_train_dqn.py` if you'd like to train the AI without considering "Hold" action.

Run `run_play_dqn_hold.py` if you'd like to see the AI play Tetris when considering "Hold" action.

Run `run_train_dqn_hold.py` if you'd like to train the AI when considering "Hold" action.

Run `run_performance.py` to see how many games and frames per second it has using randomized actions.

## Links
[Report Video]
(https://www.youtube.com/watch?v=H9yfl8hy8OA)

Explanations for statistics

[Building Controllers for Tetris](https://pdfs.semanticscholar.org/e6b0/a3513e8ad6e08e9000ca2327537ac44c1c5c.pdf)

[Tetris Agent Optimization Using Harmony Search Algorithm](https://hal.inria.fr/inria-00418954/file/article.pdf)



