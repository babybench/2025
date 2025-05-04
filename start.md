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

Other ideas, e.g. to learn goal-based behaviors, should also rely on wrapper functions rather than modifying the environments directly. You can read the Gymnasium [documentation about wrappers](https://gymnasium.farama.org/api/wrappers/) and follow [this tutorial](https://gymnasium.farama.org/tutorials/gymnasium_basics/implementing_custom_wrappers/).

### Configuration files

To facilitate the initialization of BabyBench, we provide a configuration file for each environment. You can control the environment parameters using a configuration file, which is loaded as follows:

```python
import yaml
import babybench.utils as bb_utils

with open('examples/config_test_installation.yml') as f:
    config = yaml.safe_load(f)

env = bb_utils.make_env(config)
```

Running this code creates the environment used for the installation test. You can find a list of all the configuration options in the [API](../api) page. The main parameters you need to set are described next.

#### Behavior

The ``behavior`` parameter determines the target behavior that will be tracked in the environment. This parameter can be set to ``none``, ``selftouch`` or ``handregard``. Each behavior will also load a specific MIMo version: the ``none`` and ``selftouch`` behaviors use MIMo v1 (with mitten-like hands), and the ``handregard`` behavior uses MIMo v2 (with fingers).

#### Scene

The ``scene`` parameter determines the scene that will be used in the environment. Each scene has specific objects and introduces different constraints, such as fixing MIMo to a specific pose. This parameter can be set to ``base``, ``crib`` or ``cubes``. Examples of each scene are shown below. While both behaviors can be learned in eaither scene, we recommend using the ``crib`` scene for self-touch and the ``cubes`` scene for hand regard.

<figure>
    <img src="static/images/base_scene.png" alt="Base scene">
    <figcaption>Base scene</figcaption>
</figure>

<figure>
    <img src="static/images/crib_scene.png" alt="Crib scene">
    <figcaption>Crib scene</figcaption>
</figure>

<figure>
    <img src="static/images/base_scene.png" alt="Cubes scene">
    <figcaption>Cubes scene</figcaption>
</figure>

#### Sensory modules

MIMo has four sensory modules: proprioception, vestibular system, vision, and touch. They can be enabled or disabled by setting the corresponding parameters, e.g. ``vision_active``, to ``True`` or ``False``. Additionally, each sensory module has specific parameters that can be changed in the confiuratno files, such as the resolution of the eye cameras set with ``vision_resolution``.   

#### Actuation module

The ``actuation_model`` parameter determines the actuation model that will be used to control MIMo. This parameter can be set to ``spring_damper``, ``muscle``, or ``positional``. You can decide which body parts will be actuated by setting the corresponding parameters, e.g. ``act_hands``, to ``True`` or ``False``. Alternatively, you can decide if a body part should be locked in its original position by setting the corresponding parameter, e.g. ``lock_hands``, to ``True`` or ``False``.

#### Other options

The other options that can be set in the configuration files are the folder to saving folder (``save_dir``) and the parameters of the environment (``max_episode_steps``, ``frame_skip``, ``render_size``, ``save_logs_every``), which are described in the [API](../api) page.

## Starter code examples

We provide some basic examples with starter code to help you get up and running with training MIMo using reinforcement learning. These examples are available in the ``examples`` folder of the [starter kit](https://github.com/babybench/babybench2025_starter_kit).


### Recommended configurations

Besides the aforementioned ``config_test_installation.yml`` file, we also provide a configuration files for each of the two behaviors. These are not mandatory to use, but rather recommendations that we think provide a good starting point for training MIMo.

#### Self-touch
{: .no_toc }

The configuration file for self-touch is ``config_selftouch.yml``. It uses the ``crib`` scene. All the proprioception settings are set to ``True``, whereas the vestibular and vision settings are set to ``False``. The touch observations are enabled everywhere in MIMo's body except for his eyes. The ``actuation_model`` is set to ``spring_damper``, and the actuators of MIMo's hands, fingers, arms, legs, body, and head are enabled, but not his feet or eyes, which are locked. 

A number of simplifications are available here. In particular, you can reduce the size of the action space by disabling some of the actuators, e.g. the body or legs. You can also reduce the size of the observation space by disabling some of the parameters of the proprioception module, e.g. torques and limits. Finally, you can simplify the touch observations by using a higher scale factor, which will reduce the number of touch sensors, e.g. setting ``touch_scale`` to ``5``. 

#### Hand regard
{: .no_toc }

The configuration file for self-touch is ``config_selftouch.yml``. It uses the ``cubes`` scene. All the proprioception settings are set to ``True``, whereas the vestibular and touch modalities are disabled. The visual sytem is active, with a resolution of ``64`` pixels. The ``actuation_model`` is set to ``spring_damper``, and the actuators of MIMo's hands, arms, and head are enabled, whereas his fingers, feet, legs, body, and eyes are locked.

As in the self-touch configuration, you can simplify the experiments by reducing the size of the action and observation spaces. In this case, you can also use the ``crib`` scene instead of the ``cubes`` scene. This will put MIMo in a supine position and with fewer objects in his field of view, which may make the learning of hand regard easier. 

### Random policies

In the ``examples`` folder of the [starter kit](https://github.com/babybench/babybench2025_starter_kit), you can find two code examples that execute random policies for both self-touch and hand regard. These examples are only provided to show how you can use the API to implement your own policies. They can also serve as a baseline for both behaviors, i.e. how much of his own body does MIMo touch or how often does he fixate his own hand when he moves randomly. Running the scripts ``random_selftouch.py`` or ``random_handregard.py`` will execute the random policy for a total of 10,000 timesteps by default. These scripts make use of Python's [Argument Parser](https://docs.python.org/3/library/argparse.html) to parse the command line arguments. To run the script with a different number of timesteps, you can run the following command:

```bash
python examples/random_selftouch.py --train_for=100000
```

The argument is called ``--train_for`` for consistency with the other examples described next; there is no actual training for the random policy. After running the script, you can find the training log in the ``results/self_touch/logs`` folder (or the corresponding value of ``save_dir`` in the configuration file used). You can then run an evaluation of the training log to get an estimate of the performance of the random policy.

### Intrinsic motivations

As mentioned above, a common expected approach for the competition is to use intrinsically-motivated reinforcement learning. The simplest way to do this is to use an environment wrapper, as described previously. The ``examples`` folder of the [starter kit](https://github.com/babybench/babybench2025_starter_kit) contains three scripts that can serve as starting points in this direction.

#### Template
{: .no_toc } 

The ``intrinsic_motivation_wrapper.py`` script is a template for learning an intrinsically-motivated policy. It contains the wrapper mentioned earlier, but also describes a common training loop with the Proximal Policy Optimization (PPO) algorithm of the [Stable Baselines-3](https://stable-baselines3.readthedocs.io/en/master/modules/ppo.html) library. The relevant code snippet is shown below:

```python
from stable_baselines3 import PPO

model = PPO("MultiInputPolicy", wrapped_env, verbose=1)
model.learn(total_timesteps=args.train_for)
model.save(os.path.join(config["save_dir"], "model"))
```

Running this code will create an instance of the PPO algorithm that can accommodate the observation and action spaces of the environment. The model will then be trained for a total of 10,000 timesteps by default, and saved in the ``save_dir`` folder of the configuration file.

Since the value of the intrinsic reward of this wrapper is always 0, running this script will not produce any interesting behaviors. However, you can use this script as a starting point for your own implementations of intrinsically-motivated reinforcement learning. The next two examples show how you can use the wrapper to learn a self-touch policy and a hand regard policy.

#### Self-touch
{: .no_toc }

The ``intrinsic_selftouch_count.py`` script adapts the ``intrinsic_motivation_wrapper.py`` script with a very simple approach towards learning self-touch: trying to maximize the fraction of active touch sensors in MIMo's body. The relevant code snippet is shown below:

```python
def compute_intrinsic_reward(self, obs):
    # Count the fraction of active touch sensors in MIMo's body
    intrinsic_reward = np.sum(obs['touch'] > 1e-6) / len(obs['touch'])
    return intrinsic_reward
```

Do you think this is a good approach? If you can come up with a better intrinsic reward, you can easily modify the script and train MIMo to learn self-touch. 


#### Hand regard
{: .no_toc }

The ``intrinsic_handregard_saliency.py`` script also adapts the ``intrinsic_motivation_wrapper.py`` script but aiming to learn the hand regard behavior. We postulate that the hand can be a salient object in MIMo's field of view, and thus MIMo might learn to fixate his hand in order to maximize this saliency. We come up with a simple saliency metric:

```python
from scipy.ndimage import convolve

def simple_saliency(rgb_img):
    gray_img = bb_utils.to_grayscale(rgb_img)
    # Define a simple Laplacian kernel
    laplacian_kernel = np.array([[0, -1, 0],
                                  [-1, 4, -1],
                                  [0, -1, 0]])
    # Apply the kernel using convolution
    edges = convolve(gray_img, laplacian_kernel, mode='reflect')
    # Compute saliency as sqrt of sum of squared edge intensities (normalized)
    saliency = np.sqrt(np.sum(edges**2)) / (gray_img.shape[0] * gray_img.shape[1])
    return saliency
```

And then the intrinsic reward is computed as:

```python
def compute_intrinsic_reward(self, obs):
    return simple_saliency(obs['eye_left']) + simple_saliency(obs['eye_right'])
```

Again, you can come up with a better intrinsic rewards to explain the emergence of hand regard. We encourage you to try different approaches and make a submission to the competition.


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