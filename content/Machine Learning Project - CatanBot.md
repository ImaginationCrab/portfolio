By Henry Jiang, Jeffrey Chen, Alexander Ge, Tracy Yang, Ray Dai
1. Introduction
We propose creating a convolutional neural network based model for the purpose of playing the game of Catan. By leveraging the feature-extraction capabilities of a CNN in tandem with other machine learning methods, we seek to accurately interpret complex probabilistic board states and win consistently with Catanbot. 

1.1. Literature Review
	Previous architectures consisting of CNN models finetuned on reinforcement learning with MCTS for state evaluation proved extremely effective by AlphaZero for Go and Chess (Silver et al 2017). For Catan in particular, strategies such as Monte-Carlo Tree Search (MCTS) (Szita et al 2009) and Markov Chains (Nagel et al 2021) have shown promise as well in modeling Catan in particular, with random walks helping to identify probabilistic winning moves. Deep reinforcement learning strategies have also been applied to Catan to achieve high level performance, demonstrating the applicability yet relatively untapped potential of machine learning methods for playing Catan (Charlesworth 2022).

1.2. Dataset
Our dataset consists of 43,947 anonymized 4-player Catan games scraped from the site Colonist.io, an online site for playing Catan against other human or AI players. Each game is encoded in a JSON file, consisting of the initial board state and every move and action taken by the players across the course of the game.
https://github.com/Catan-data/dataset/releases/tag/v1.0.0

Problem and Motivation
Catan offers a unique set of challenges compared to deterministic games such as chess and Go where supervised learning has displayed success in mastering the game; beyond having 4 players rather than 2, Catan contains random chance through the randomized starting state of the board and dice rolls for resources. These rolls determine the resources that a player receives each turn, potential loss of resources, and card stealing through robber movement. Furthermore, Catan has the important game mechanic of trades, which present an combinatorially exploding set of circumstances for an agent to consider in every turn. 
	Our project seeks to apply supervised learning and other concepts to determine the effectiveness of machine learning in accurately modeling outcomes in non-deterministic game states and games with multi-player driven interactions.

Methods
3.1. Data Preprocessing
As our data comes from Colonist.io in JSON form, we plan on adapting this data to allow our model to reconstruct the present game state across every turn of the game played, and use the winning player and point leader across the course of the game as our label for our model to extrapolate winning and losing strategies from. We will need a method of converting unprocessed data to a feature vector for our model and return an action that would be playable on the website for the purpose of testing our model. We plan on using Pytorch for our CNN implementation.

3.2. Algorithms
	We plan on implementing a CNN architecture as they are uniquely suited for taking the board state in as a feature map and determining spatial patterns and the best action for ideal probabilistic outcomes. Due to potential time constraints and difficulties in data preprocessing, we will only apply a CNN to our data. However, if time allows, we will expand on our implementation by adding in MCTS for the purpose of current state evaluation similar to the implementations of AlphaZero. Reinforcement learning is another possibility for finetuning our model, allowing it to play itself for thousands of iterations to improve upon the base model trained via CNN.

Results
As our agent is trained on games scraped from Colonist.io, we would be able to adapt our model to play games on the site by scraping the current game state and passing it to our model. We plan to test our model against bots that make random moves or heuristic based (greedy, MCTS) moves as a control to see if our agent is able to win against them more than the expected rate of 25%, and we can also test our model against real players in online games in the same manner.
 	We will also perform ablation studies, removing specific capabilities like board state evaluations or reducing MCTS depth to assess whether machine learning has a measurable improvement in Catanbot’s performance. Furthermore, we can assess our model’s capabilities qualitatively, comparing the model’s choices in settlement placement against that of top players in the same situation or crafting puzzles where a specific move leads to an objective win scenario or winning position.

References
Charlesworth, H., (2022). Learning to Play Settlers of Catan with Deep Reinforcement Learning. https://settlers-rl.github.io/
MR. MUCHO BUCHO Game Data (2025) 43,947 anonymized 4-player Catan games. https://github.com/Catan-data/dataset 
Nagel, L. (2021). Analysis of ‘The Settlers of Catan’ Using Markov Chains.  https://repository. tcu.edu/entities/publication/8c4915c9-0127-458d-a53c-13482fdbefa6
Silver, D. et al, (2017). Mastering the game of Go without human knowledge. https://www.nature .com/articles/nature24270
Szita, I. et al, (2009). Monte-Carlo Tree Search in Settlers of Catan. https://link.springer.com/ chapter/ 10.1007/978-3-642-12993-3_3