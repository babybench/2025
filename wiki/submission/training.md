---
title: Training
parent: Prepare a submission
layout: default
nav_order: 0
---

# Training

Participants are expected to train MIMo within the environments provided in BabyBench benchmark. Each environment is designed to elicit specific developmental behaviors, and the core challenge of the competition lies in enabling the agent to learn these behaviors autonomously through interaction and experience. While the environments are built using the Gymnasium framework, they are deliberately designed without extrinsic rewards, in order to encourage the use of intrinsic motivation, unsupervised learning, or other developmentally inspired mechanisms.  

We recommend carrying out the training using the standard Gymnasium API, which includes the `env.reset()` method to initialize the environment and the `env.step(action)` method to apply an action and receive the resulting observation, termination flags, and (empty) reward. Participants are responsible for implementing their own training loop using this interface (but see [examples](../start/examples/) for possible code starting points). There are no constraints on the learning algorithm, so long as the agent interacts with the environment using the correct API. Whether participants choose to use reinforcement learning, self-supervised learning, predictive modeling, or handcrafted mechanisms is entirely up to them.

To support analysis and evaluation, an information history is maintained in the environments and stored as a training log automatically (every 100 episodes in the default `config.yml`). This log records relevant statistics about the agent’s behavior and learning progress over time. These logs must be uploaded for the evaluations, so please make sure to prevent overriding them.