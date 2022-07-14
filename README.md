# GAME: Nim
## AI that teaches itself to play Nim through reinforcement learning.

Using a Q-learning algorithm to teach an ai to play Nim. Nim is a game where there are piles of objects from 4 piles and each player takes turns taking a non zero number of objects out of a chosen pile. The person who ends the game by taking the last tile(s) loses the game. Compile play.py to play against the ai

There’s some simple strategy you might imagine for this game: if there’s only one pile and three objects left in it, and it’s your turn, your best bet is to remove two of those objects, leaving your opponent with the third and final object to remove. But if there are more piles, the strategy gets considerably more complicated!

In this problem, we create an AI that uses reinforcement learning to learn the game's tactics. Our AI will learn which actions to take and which acts to avoid by continuously playing against itself and learning from its mistakes.

In particular, we’ll use Q-learning for this project. In Q-learning, we try to learn a reward value for every pair. An action that loses the game will have a reward of -1, an action that results in the other player losing the game will have a reward of 1, and an action that results in the game continuing has an immediate reward of 0, but will also have some future reward.

How will we represent the states and actions inside of a Python program? A “state” of the Nim game is just the current size of all of the piles. A state, for example, might be `[1, 1, 3, 5]`, representing the state with 1 object in pile 0, 1 object in pile 1, 3 objects in pile 2, and 5 objects in pile 3. An “action” in the Nim game will be a pair of integers `(i, j)`, representing the action of taking `j` objects from pile `i`. So the action `(3, 5)` represents the action “from pile 3, take away 5 objects.” Applying that action to the state `[1, 1, 3, 5]` would result in the new state `[1, 1, 3, 0]` (the same state, but with pile 3 now empty).

Recall that the key formula for Q-learning is below. Every time we are in a state `s` and take an action `a`, we can update the Q-value `Q(s, a)` according to:

`Q(s, a) <- Q(s, a) + alpha * (new value estimate - old value estimate)`

In the above formula, `alpha` is the learning rate (how much we value new information compared to information we already have). The `new value estimate` represents the sum of the reward received for the current action and the estimate of all the future rewards that the player will receive. The `old value estimate` is just the existing value for `Q(s, a)`. By applying this formula every time our AI takes a new action, over time our AI will start to learn which actions are better in any state.