**Project One: Navigation**

**Introduction-Project Details**

This project, will allow a user train an agent to navigate (and collect bananas!) in a large, square world.


A reward of +1 is provided for collecting a yellow banana, and a reward of -1 is provided for collecting a blue banana. Thus, the goal of your agent is to collect as many yellow bananas as possible while avoiding blue bananas.

The state space has 37 dimensions and contains the agent&#39;s velocity, along with ray-based perception of objects around agent&#39;s forward direction. Given this information, the agent must learn how to best select actions. Four discrete actions are available, corresponding to:

- **0**  - move forward.
- **1**  - move backward.
- **2**  - turn left.
- **3**  - turn right.

The task is episodic, and in order to solve the environment, your agent must get an average score of +13 over 100 consecutive episodes.

**Getting Started**

The environment is comprised of a vector of 37 discrete observations at each time step that is passed from the environment &quot;brain&quot; to an agent.  The agent selects one of the four actions with the intention of maximizing the amount of award received for collecting yellow bananas and avoiding the blue bananas.  The agent collects the state, action and reward information as it steps through the environment until it receives an indicator that an episode of the game is done or that it has maxed out the number of steps (limited at 10000).   The collected state, action, and reward information is stored in an experience queue that is used to train the agent to maximize its reward over an episode.

The environment is considered solved once an average score of 13 is achieved for 100 episodes.

Both the model and the agent modules come in two flavors each making a total of four combinations of models and agent types.  The two models are a (1): a standard two layer network of 64 nodes in the two layers and relu activation (states x 64 x 64 x actions with relu activation) essentially provided with the course and (2): a dueling network modeled after the Google team&#39;s design in the paper Dueling Architectures for Deep Reinforcement Learning by Wang et all.  The dueling architecture has two streams.  One stream is a state to value network and the other is the incremental value of each action.  The two streams are combined to aggregate the two streams at the output to estimate a Q function at output.  The network has been proven to more quickly provide the correct action during policy evaluation by immediately determining which states are more valuable and adding additional discernment regarding action for more valuable states (please see the original paper).

The two agent models are (1): standard deep q learning agent with fixed queue learning and experience recall; and (2): deep q learning agent with fixed que learning, experience recall and double q learning.  The fixed queue learning capability uses two networks, one for determining the state action choice and one to provide the target for which learning takes place.  The target is updated less frequently than the local network to avoid destabilizing feedback from one network to the other.  The experience recall capability stores the action reward sequences in memory for training.  The experiences are sampled randomly in batches, every few timesteps and used for training.  The experience recall method turns the learning problem into deep network supervised learning and avoids there being too much correlation between successive state action reward sequences.  The added capability of double q learning uses the local network to provide the target action value from the maximum value action provided by the target network.

**Installing Dependencies**

**Unity Machine Learning Agents (ML-Agents)** is an open-source Unity plugin that enables games and simulations to serve as environments for training intelligent agents. The unity ML-Agents environment is installed on Windows 10 using the Unity installation instructions.  The banana environment and the unity agent folders are included in the root of the project directory.  Other dependencies are imported as part of a Jupyter project notebook.  The dependencies include Pytorch, numpy, Matplotlib, collections, and random.  In addition to these standard python packages, there are two custom python code modules that are imported which comprise the bulk of the agent code.  One module is named: model.py and contains a Pytorch neural network model for the agent&#39;s deep reinforcement learning.  The other module is named dqn\_agent.py.  Both modules rely substantially on the code provided in the class for deep q learning.

**Instructions**

Training the network is simple.  Make certain that the environment files are in the root directory.  Open the Jupyter Notebook for the particular combination of model and agent.  For example, open the NavigationDuelDouble notebook to operate the dueling network model with double q learning (all agents use experience recall and fixed q learning as well).  The make certain that the dueling model is titled model.py so that the agent can access the model appropriately.  Finally make certain that the double q learning agent is named dqn\_agent.py.  Start the leaning by running the code that includes the dqn() function.

The output will be first a description of the environment then followed by a running list of episodes and the average value of the game.  The inputs are set to default to 2000 episodes, but the routine should learn to achieve a score more than 13 in less than 500 episodes.

