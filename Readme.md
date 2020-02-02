# Continuous Control
---

## Introduction of the Environment

For this project, I will work with the Reacher environment.
https://github.com/Unity-Technologies/ml-agents/blob/master/docs/Learning-Environment-Examples.md#reacher

In this environment, a double-jointed arm can move to target locations. A reward of +0.1 is provided for each step that the agent's hand is in the goal location. Thus, the goal of your agent is to maintain its position at the target location for as many time steps as possible.

The observation space consists of 33 variables corresponding to position, rotation, velocity, and angular velocities of the arm. Each action is a vector with four numbers, corresponding to torque applicable to two joints. Every entry in the action vector should be a number between -1 and 1.

Set-up: Double-jointed arm which can move to target locations.<br> 
Goal: The agents must move its hand to the goal location, and keep it there.<br> 
Agents: The environment contains 1 agent with same Behavior Parameters.<br> 
Agent Reward Function (independent):
* +0.1 Each step agent's hand is in goal location.<br> 

Behavior Parameters:
* Vector Observation space: 33 variables corresponding to position, rotation, velocity, and angular velocities of the two arm Rigidbodies.<br> 
* Vector Action space: (Continuous) Size of 4, corresponding to torque applicable to two joints.<br> 
* Visual Observations: None.<br> 

Reset Parameters: Five
* goal_size: radius of the goal zone
    * Default: 5
    * Recommended Minimum: 1
    * Recommended Maximum: 10
* goal_speed: speed of the goal zone around the arm (in radians)
    * Default: 1
    * Recommended Minimum: 0.2
    * Recommended Maximum: 4
* gravity
    * Default: 9.81
    * Recommended Minimum: 4
    * Recommended Maximum: 20
* deviation: Magnitude of sinusoidal (cosine) deviation of the goal along the vertical dimension
    * Default: 0
    * Recommended Minimum: 0
    * Recommended Maximum: 5
* deviation_freq: Frequency of the cosine deviation of the goal along the vertical dimension
    * Default: 0
    * Recommended Minimum: 0
    * Recommended Maximum: 3
Benchmark Mean Reward: 30

## Solving the Environment

I have chosen the first version of the environent with single agent. The task is episodic, The agent must get an average score of +30 over 100 consecutive episodes.

Because the action space is continuous, I used DDPG: Deep Deterministic Policy Gradient, Continuous Action-space which is am implementation of Actor-Critic Methods to solve the environment. the Actor takes state S and output the distributions over actions while the critic takes state and output state value function. We use Use the critic to calcuate the advantage function A(s,a) to use it as baseline to train the Actor. Each network has 2 copies, one local and target where I apply soft update for the parameters.

## The Environment preparation

To set up your python environment to run the code in this repository, follow the instructions in the link below.<br>
https://github.com/udacity/deep-reinforcement-learning#dependencies

Download the Unity Environment Version 1: One (1) Agent
* Linux: https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/one_agent/Reacher_Linux.zip
* Mac OSX: https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/one_agent/Reacher.app.zip
* Windows (32-bit): https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/one_agent/Reacher_Windows_x86.zip
* Windows (64-bit): https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/one_agent/Reacher_Windows_x86_64.zip

## Hyper-Parameter tuning

BUFFER_SIZE = int(1e6)           $\;\;\;\;\;\;$ # replay buffer size<br>
BATCH_SIZE = 128                 $\;\;\;\;\;\;$ # minibatch size<br>
GAMMA = 0.99                     $\;\;\;\;\;\;$ # discount factor<br>
TAU = 1e-3                       $\;\;\;\;\;\;$ # for soft update of target parameters<br>
LR_ACTOR = 1e-3                  $\;\;\;\;\;\;$ # learning rate of the actor<br>
LR_CRITIC = 1e-3                 $\;\;\;\;\;\;$ # learning rate of the critic<br>
WEIGHT_DECAY = 0                 $\;\;\;\;\;\;$ # L2 weight decay<br>

LEARN_EVERY = 20                 $\;\;\;\;\;\;$ # learning timestep interval<br>
LEARN_NUM   = 10                 $\;\;\;\;\;\;$ # number of learning passes<br>
GRAD_CLIPPING = 1.0              $\;\;\;\;\;\;$ # Gradient Clipping<br>

Ornstein-Uhlenbeck noise parameters:<br>
OU_SIGMA  = 0.01<br>
OU_THETA  = 0.15<br>
EPSILON       = 1.0              $\;\;\;\;\;\;$ # for epsilon in the noise process (act step)<br>
EPSILON_DECAY = 1e-6<br>



```python

```
