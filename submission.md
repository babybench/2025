---
title: Prepare a submission
layout: default
nav_order: 4
---

# Prepare a submission
{: .no_toc }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}


## Training

Participants are expected to train MIMo using the environments provided. Each environment is designed to elicit specific developmental behaviors, and the core challenge of the competition lies in enabling the agent to learn these behaviors autonomously through interaction and experience. While the environments are built using the Gymnasium framework, they are deliberately designed without extrinsic rewards, in order to encourage the use of intrinsic motivation, unsupervised learning, or other developmentally inspired mechanisms.

We recommend carrying out the training using the standard Gymnasium API as described in the [API page](../api), which includes the `env.reset()` method to initialize the environment and the `env.step(action)` method to apply an action and receive the resulting observation, termination flags, and (empty) reward. Participants are responsible for implementing their own training loop using this interface (but see [starter code examples](../start/) for possible code starting points). There are no constraints on the learning algorithm, so long as the agent interacts with the environment using the correct API. Whether participants choose to use reinforcement learning, self-supervised learning, predictive modeling, or handcrafted mechanisms is entirely up to them. We

To support analysis and evaluation, an information history is maintained in the environments and stored as a training log automatically (every 1000 episodes in the default `config` file). This records relevant statistics about the agent’s behavior and learning progress over time. These logs must be uploaded for the evaluations, so please make sure to prevent overriding them. 


## Evaluation

Once you have finished training MIMo, you can run an evaluation by modifying the ``evaluation.py`` file to include your trained model. This will create an instance of the `Evaluation` class from the the ``babybench/eval.py`` file,  which provides a simple interface to evaluate the training progress and the learned the behaviors learned by MIMo. Running the evaluation will generate logs and videos of the learned behaviors, which you can upload to the submission page (see below).


## Checklist

Before uploading your submission, please make sure to check the following items:

- [x] Extended abstract of up to 2 pages with a clear overview of your approach, including a description of the learning method used and a preview of the results.

- [x] Training log file called `training.pkl` automatically generated during training. Located in the `logs` folder within the directory specified in the `config.yml` file.

- [x] Trajectory log files called `episode_i.pkl` automatically generated during the evaluation. Located in the `logs` folder within the directory specified in the `config.yml` file.

- [ ] (Optionally) Link to the videos of the learned behavior called `episode_i.avi` automatically generated during the evaluation. Located in the `videos` folder within the directory specified in the `config.yml` file. *Note: videos should be uploaded to a personal server or cloud storage.*

- [ ] (Optionally) Link to the code used to train the model. *Note: code should be uploaded to a repository.*

If you have any questions about the submission files, please don't hesitate to [contact us](mailto:fcomlop@gmail.com).



## Upload your submission

Submissions must be made through the [PaperPlaza](https://ras.papercept.net/) system.

When you are ready to submit, head over to [PaperPlaza](https://ras.papercept.net/), search for ICDL and choose “Submit a Contribution to ICDL”. Scroll down to the BabyBench Competition and choose Submit. All authors are requires to have a [PIN](https://ras.papercept.net/conferences/scripts/pinwizard.pl).

---

### [Next page: Competition guidelines](../competition)
{: .no_toc }