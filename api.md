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

## Basic usage

BabyBench uses the standard MIMo interface with the Gymnasium API:

```python
import gymnasium as gym
import mimoEnv

env = gym.make("BabyBench-SelfTouch")
obs, _ = env.reset()

done = False
while not done:
    action = select_action(obs)
    obs, reward, terminated, truncated, info = env.step(action)
    done = terminated or truncated
```

Users are **not** expected to modify any of the BabyBench or MIMo code, but rather to write their own training loops using the provided API to interact with the environments. 

## Configuration

To facilitate the initialization of BabyBench, users can control the environment parameters using a configuration file:

```python
import yaml
import babybench.utils as bb_utils

with open('config.yml') as f:
    config = yaml.safe_load(f)

env = bb_utils.make_env(config)
```

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