---
published: true
title: "Deep Reinforcement Learning Intro"
date:   2018-02-19 00:00:00 +0100
author_profile: true
mathjax: true
categories:
  - Deep Learning
tags:
  - Reinforcement Learning
---

In this post I'm gonna a make a small intro to the Deep Reinforcement Learning field. This intro is based on the topics given in the [MIT 6.S094: Deep Reinforcement Learning](https://www.youtube.com/watch?v=MQ6pP65o7OM).

**Reinforcement learning** is a general purpose framework for decision making used as part of the design of artificial devices to interact with the environment. The **agent** is programmed for achieving a **goal** through a set of temporal **actions** that change the **state** of the world receiving a measured **reward** that can be positive or negative. The agent is programmed for maximizing the reward.

![RL components]({{ site.url }}/assets/images/2018-02-19-deep-reinforcement-learning-intro/RL.png){: width="150px" style="float: right;margin-right: 7px;margin-top: 7px;"} **Sensors** take **data** from the **environment** and a model make a **feature extraction** of the elements important for building a **representation hierarchy** of the environment. A set of **machine learning** techniques are applied to convert the features into **knowledge** building a *taxonomy* with the simple and useful information valid for the decision process. With this knowledge, the agent makes the **reasoning** for inferring conclusions about the knowledge and makes a **planning** based on the goals, materialized in a maximization of a *reward function*. From the planning and **action** is derived and the **effector** apply the decided actions over the environment.

How much of this process can be learned in an end-to-end fashion? Up to know, deep learning techniques have enhanced the building of systems able to learn from sensor data to knowledge. The challenge right now is to broaden the application of deep learning to the stages of reasoning, planning and action.

# Kind of tasks the Artificial Intelligence agents can learn

We sort by order of difficulty the tye of task that we would like to solve in AI. Some of them have been already solved, others are openened problems.

1. Formal tasks: board games, puzzles, math & logic problems
2. Expert tasks: medical diagnosis, engineering, scheduling, etc.
3. Mundane tasks: speech recognition, written language, perception, walking, object manipulation, etc.
4. Human tasks: Awareness of self, emotion, imagination, morality, subjective experience, high-level reasoning, conciousness

# Types of Machine Learning

Machine learning can be done mainly by two completely independent categories: supervised learning & unsupervised learning. 

**Supervised learning** uses a set of labeled examples to learn. It requires the knowledge of an expert for learning.

**Unsupervised learning** does not require the information given by an expert to learn. It learns from its own experience.

**Reinforcement learning** is a way of learning from the interaction with the environment. It learns from sparse reward data in a supervised manner. It uses into its favor the assumption that the physical world evolves insome sort of predictical way. It constructs a internal model of the environment that allows the formation of strategies for achieving its own goals. The basic constituents of reinforcement learning are the agent, the environment where it acts, the internal state of the agent in every time step, the observation of the environment, the reward function materializing the goals and the actions takes by the agent based on the internal model of the environment aligned with the consecution of the maximization of the reward.

# Interaction between the agent and the environment

Image below shows the type of interaction between the agent and the environment. The agent takes an action, makes an observation of the environment and updates its internal state and the reward obtained from the environment. 

![Agent - Environment Interaction]({{ site.url }}/assets/images/2018-02-19-deep-reinforcement-learning-intro/agent_env.png)

This interaction produces a succession of **action, reward, state**s. This succession is a **Markov decision process**, a succession of the type $$ s_0, a_0, r_1, s_1, a_1, r_2, ..., s_{n-1}, a_{n-1}, r_n, s_n $$ until reaching a terminal state $$ s_n $$.

# Major Components of a Reinforcement Learning Agent

* Policy: is the agent behavioural function
* Value function: how good is the state and/or action
* Model: environment representation

The strategy of the agent is always aligned with the maximization of the reward.

## Value function
The value function encodes the reward that the agent is likely to receive in the future.

$$ R = r_t + r_{t+1} + r_{t+2} + r_n $$

In real world, future rewards are not deterministic, they are conceived as an expectation. Due to this fact, they cannot be summed up with the actual rewards, and they have to be discounted. So, in a stochastic environment the reward can be represented as:

$$ R_t = r_t + \gamma r_{t+1} + \gamma^2 r_{t+2} + ... = r_t + \gamma ( r_{t+1} + \gamma (r_{t+2} + ... )) = r_t + \gamma R_{t+1} $$

# Q-Learning

Q-learning is a model-free reinforcement learning technique. It is able to compare the expected utility of the available actions (for a given state) without requiring a model of the environment. Additionally, Q-learning can handle problems with stochastic transitions and rewards, without requiring adaptations.

$$ Q $$ approximates $$ Q^* $$, the Dynamic Programming discrete Bellman Optimality equation:

$$ Q_{t+1}(s_t, a_t) = Q_t(s_t, a_t) + \alpha (R_{t+1}  + \gamma \max_a Q_t(s_{t+1}, a) - Q_t(s_t, a_t)) $$

where: $$ Q_t(s_t, a_t) $$ is the old state, $$ \alpha $$ the learning rate and $$ R_{t+1} $$ the discounted reward.

# Exploration vs Exploitation

These two concepts and the exact equilibrium between them are the key ingredients of reinforcement learning in stochastic environments. **Exploration** allows try of different actions not previously tried in order to find new strategies of doing things. ** Exploitation ** goes deeper into the good strategies. At first is good to explore a lot and as training advances is good to center every time more in the strategies tht work best.

Deep learning is very good approximating Q tables. Exhaustive Q tables are impossible to save completely in memory due to the massive amount of actions and states combinations.

Deep learning and Reinforcement Learning form a general purpose AI through efficient generalizable learning of the optimal things to do given a formalized set of actions and states.

# Intelligence s Understanding

Intelligence is the hability to accomplish complex goals and Understanding is the hability to turn complex information into simple and useful information.

# Deep Q-network 

[Playing Atari with Deep Reinforcement Learning](https://arxiv.org/abs/1312.5602) presented the DQN. The network was trained with a very similar approach of a supervised training. 

Being the Bellman equation $$ Q(s,a) = r + \gamma \max_{a'} Q(s',a') $$, they used as a loss function the expectation of the squared error $$\mathbb{E} [(r + \gamma \max_{a'} Q(s',a') - Q(s,a))^2 ] $$. Being $$ r  + \gamma \max_{a'} Q(s',a') $$ the target.

They used a set of "tricks" to make it work:

* In order to avoid that the system overfits over the particular actual learning experience, the training was not done using the actual experience but over a minibatch of randomly chosen previously lived and stored experiences.
* In order to increase the stability of the training, the target network was only updated every 1000 steps. In this way, the changes in the cost function were more smooth.
* Reward clipping was applied in order to fx it to the interval $$ [-1, +1] $$
* Action only took place every four steps, skipping the rest, in order also to soften the action over the environment.

## Deep Q-learning algorithm

As mentioned above, the loop controls the saving of new experiences and training is done using a minibatch of randomly chosen previously saved experiences, not on the actual one.

```
initialize replay memory D
initialize act-value function Q with random weights
observe initial state
repeat
  select an action a
    with probability $$ \epsilon $$ select random action (exploration)
    otherwise select $$\argmax_{a'} Q(s,a') $$ (exploitation)
  carry out action a
  observe reward r and new state s'
  store experience <s, a, r, s'> in replay memory D
  
  sample random transitions <ss, aa, rr, ss'> from replay memory D
  calculate target for each minibatch transition
  if ss' is terminal state then tt = rr
  otherwise $$ tt = rr + \gamma \max_{a'}Q(ss', aa') $$
  train Q network using $$ (tt - Q(ss, aa))^2 $$ as loss
  s = s'
until terminated
```
# Alpha-zero. Learning from zero to play Go better than humans.

The Game of Go is the most challenging of all the existing board games. With more than $$ 10^170 $$ different possible positions has a complexity far greater than chess.

In [Mastering the game of Go without human knowledge](https://www.nature.com/articles/nature24270) DeepMind company introduced a Reinforcement Learning algorithm that was able learn to play Go and achieve human performance and beat previously best automatic algorithms by only playing against itself with no prior knowlegde of the game but only the rules.

This algorithm used a Montecarlo Tree seach (MCTS) combined with a convolutional neural network to get the intuitions about whic positions to expland. This combined strategy was used to balance exploration vs exploitation equilibria.

The tricks used in the training that make possible this breakthrough were:

* MCTS intelligent look-ahead to improve the value estimation of play options
* Multitask learning of the neural network used outputing next move probabilities and probability of winning of actual position.
* An improved neural network design using a ResNet architecture.




