---
title: API
layout: default
nav_order: 3.5
---

# API
{: .no_toc }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}



## Configuration


The list of available parameters that can be defined in the configuration files is the following:

| Name        | Default          | Options | Description |
|:------------|:-----------------|:--------|:------------|
| `save_dir` | | | |
| `behavior` | | | |
| `max_episode_steps` | | | |
| `frame_skip` | | | |
| `render_size` | | | |
| `save_logs_every` | | | |
|:------------|:-----------------|:--------|:------------|
| `proprio_velocity` | | | |
| `proprio_torque` | | | |
| `proprio_limits` | | | |
| `proprio_actuation` | | | |
|:------------|:-----------------|:--------|:------------|
| `vestibular_active` | | | |
|:------------|:-----------------|:--------|:------------|
| `vision_active` | | | |
| `vision_resolution` | | | |
|:------------|:-----------------|:--------|:------------|
| `touch_active` | | | |
| `touch_scale` | | | |
| `touch_function` | | | |
| `touch_response` | | | |
| `touch_hands` | | | |
| `touch_fingers` | | | |
| `touch_arms` | | | |
| `touch_feet` | | | |
| `touch_legs` | | | |
| `touch_body` | | | |
| `touch_head` | | | |
| `touch_eyes` | | | |
|:------------|:-----------------|:--------|:------------|
| `actuation_model` | | | |
| `act_hands` | | | |
| `act_fingers` | | | |
| `act_arms` | | | |
| `act_feet` | | | |
| `act_legs` | | | |
| `act_body` | | | |
| `act_head` | | | |
| `act_eyes` | | | |
| `lock_hands` | | | |
| `lock_fingers` | | | |
| `lock_arms` | | | |
| `lock_feet` | | | |
| `lock_legs` | | | |
| `lock_body` | | | |
| `lock_head` | | | |
| `lock_eyes` | | | |

## Environments

### Self-touch

### Hand regard

## Sensory observations

### Proprioception

### Vestibular

### Vision

### Touch

## Actuation models

### Spring-damper model

### Muscle model

### Positional model

## Evaluation

## File structure

The BabyBench 2025 starter kit contains the following files and folders:

- ``babybench``: a folder with BabyBench auxiliary code
    - ``build_xml.py``: a script to read configuration files and build MIMo XML files
    - ``eval.py``: a script with the evaluation class and methods
    - ``utils.py``: a script with auxiliary functions
- ``examples``: a folder with starter code examples
    - ``config_test_installation.yml``: a configuration file for the installation test
    - ``config_selftouch.yml``: a recommended configuration file for the self-touch behavior
    - ``config_handregard.yml``: a recommended configuration file for the hand regard behavior
    - ``random_selftouch.py``: a starter code for a random self-touch policy
    - ``random_handregard.py``: a starter code for a random hand regard policy
    - ``intrinsic_motivation_wrapper.py``: a starter code for training a generic policy that uses intrinsic motivations
    - ``intrinsic_selftouch_count.py``: a starter code for training a self-touch policy to maximize the number of touched sensors
    - ``intrinsic_handregard_saliency.py``: a starter code for training a hand regard policy to maximize visual saliency
    - ``goal_based_wrapper.py``: a starter code for training a generic policy that uses goal-based learning
    - ``goal_selftouch_sensors.py``: a starter code for training a self-touch policy to maximize the number of touched sensors
    - ``goal_based_handregard.py``: a starter code for training a hand regard policy to maximize visual saliency
- ``MIMo``: the MIMo repository
- ``results``: a folder to store the results of the training and evaluations
    - ``test_installation``: a folder with the results of the installation test (created after running ``test_installation.py``)
        - ``logs``: a folder with the results of the self-touch training (created after running ``random_selftouch.py``)
            - ``training.pkl``: the training logs generated during the installation test
        - ``videos``: a folder with the rendered videos of the self-touch training (created after running ``random_selftouch.py``)
            - ``test_installation.avi``: the rendered video of the installation test
        - ``scene.xml``: the MIMo XML file with the installation test
- ``babybench.def``: a Singularity definition file to build the container
- ``evaluation.py``: a script to evaluate the performance of a policy
- ``LICENSE``: the license file
- ``README.md``: a README file with installation and usage instructions
- ``requirements.txt``: a list of Python packages required to run the code
- ``test_installation.py``: a script to test the installation


---

### [Next page: Prepare a submission](../submission) 
{: .no_toc }