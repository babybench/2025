---
title: Getting started
layout: default
nav_order: 3
---

# Getting started
{: .no_toc }

The aim for BabyBench is to train MIMo to achieve the target behaviors (self-touch and hand regard) without any external supervision, i.e. without extrinsic rewards. How do you think infants learn these skills autonomously? 

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}


## After installation

If you successfully [installed BabyBench](../installation) and ran the installation test, you should find a short video in the folder ``results/test_installation/videos`` of MIMo in his base environment.  


You can also run a short evaluation of the installation test:
```bash
python evaluation --config=examples/config_test_installation.yml --episodes=1 --duration=100
```

We recommend you to take some time to explore the folder structure ([descrbed here](../api/#file-structure)). Inside the ``results/test_installation`` folder, you will find 2 folders: ``videos`` and ``logs``, and a ``scene.xml`` file (read the [API](../api) page for details). The ``video`` folder should contain the video of the installation test and the video of the evaluation (if you ran it). The ``logs`` folder  should contain a log file called ``training.pkl`` generated during the installation test and a log file called ``evaluation_0.pkl`` generated during the evaluation. These are pickled files; you can open them with the [pickle](https://docs.python.org/3/library/pickle.html) module in Python, for example: 

```python
import pickle
with open('results/test_installation/logs/training.pkl', 'rb') as f:
    training_log = pickle.load(f)
print(training_log)
```

This should only print the following:

```
[{'steps': 0}]
```

In the future, these logs will contain a dictionary with the information collected during training. To know more about the logs, you can read the [API](../api) page.

## Basic usage

### Initialization

You can initialize the base BabyBench environment as a regular Gymnasium environment. Create a file called ``test_env.py`` with the following code:

```python
import gymnasium as gym
import mimoEnv

env = gym.make("BabyBench")
obs, _ = env.reset()
print(obs)
```

And then run the following command on your console to initialize the environment and print an observation:

```bash
python test_env.py
```

This will print an observation of the environment, which is a long dictionary with the following keys: ``observation``, ``touch``, ``eye_left``, ``eye_right``, and ``vestibular``. Details about the observations are provided in the [API](../api) page.

### Simulations

BabyBench uses the standard Gymnasium API for simulations. You can add the following code to your script to run a full episode on the environment (note: this will run for a default of 1000 steps). 

```python
done = False
while not done:
    # TODO: REPLACE WITH YOUR ACTION SELECTION MODEL
    # action = select_action(obs)
    action = env.action_space.sample()
    obs, reward, terminated, truncated, info = env.step(action)
    done = terminated or truncated
```

### Wrapper functions

**You are not expected to modify any of the BabyBench or MIMo code**, but rather to write your own training loops using the provided [API](../api) to interact with the environments. In particular, the BabyBench environments always return extrinsic rewards of 0, because the focus of the competition is to train the agents to perform the desired behaviors without any external supervision. To use intrinsic rewards, you can use write a wrapper function:

```python
class Wrapper(gym.Wrapper):
    def __init__(self, env):
        super().__init__(env)

    def compute_intrinsic_reward(self, obs):
        # TODO: REPLACE WITH YOUR INTRINSIC MOTIVATION HERE
        intrinsic_reward = 0
        return intrinsic_reward

    def step(self, action):
        obs, extrinsic_reward, terminated, truncated, info = self.env.step(action)
        intrinsic_reward = self.compute_intrinsic_reward(obs)
        total_reward = intrinsic_reward + extrinsic_reward # extrinsic reward is always 0  
        return obs, total_reward, terminated, truncated, info

    def reset(self, **kwargs):
        return self.env.reset(**kwargs)
```

Other ideas, e.g. to learn goal-based behaviors, should also rely on wrapper functions rather than modifying the environments directly.

### Configuration files

To facilitate the initialization of BabyBench, we provide a configuration file for each environment. You can control the environment parameters using a configuration file, which is loaded as follows:

```python
import yaml
import babybench.utils as bb_utils

with open('examples/config_test_installation.yml') as f:
    config = yaml.safe_load(f)

env = bb_utils.make_env(config)
```

Running this code would create the environment used for the installation test. You can find a list of all the configuration options in the [API](../api) page. The main parameters you need to set are described next.

#### Behavior



#### Scene

#### Sensory modules

#### Actuation module

#### Other options

The other options that can be set in the configuration files are the folder to saving folder (``save_dir``) and the parameters of the environment (``max_episode_steps``, ``frame_skip``, ``render_size``, ``save_logs_every``), which are described in the [API](../api) page.

## Starter code examples

We provide some basic examples with starter code to help you get up and running with training MIMo using reinforcement learning. These examples are available in the ``examples`` folder of the [starter kit](https://github.com/babybench/babybench2025_starter_kit).


### Configuration files

### Random policies

#### Self-touch
{: .no_toc }

#### Hand regard
{: .no_toc }

### Intrinsic motivations

#### Template
{: .no_toc } 

#### Self-touch
{: .no_toc }

#### Hand regard
{: .no_toc }


### Goal-based

#### Template
{: .no_toc }

#### Self-touch
{: .no_toc }

#### Hand regard
{: .no_toc }

---

### [Next page: API](../api)
{: .no_toc }