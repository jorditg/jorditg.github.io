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

