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

BabyBench uses the standard MIMo interface with the Gymnasium API:

```python
import gymnasium as gym
import mimoEnv

env = gym.make("BabyBench")
obs, _ = env.reset()

done = False
while not done:
    action = select_action(obs)
    obs, reward, terminated, truncated, info = env.step(action)
    done = terminated or truncated
```

However, **you are not expected to modify any of the BabyBench or MIMo code**, but rather to write your own training loops using the provided [API](../api) to interact with the environments. To facilitate the initialization of BabyBench, you can control the environment parameters using a configuration file:

```python
import yaml
import babybench.utils as bb_utils

with open('examples/config_test_installation.yml') as f:
    config = yaml.safe_load(f)

env = bb_utils.make_env(config)
```


Running this code would create the environment used for the installation test. You can find a list of all the configuration options in the [API](../api) page. The main parameters you need to set are described next:

### Behavior

### Scene

### Sensory modules

### Actuation module

### Other options

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