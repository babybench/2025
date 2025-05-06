---
title: API
layout: default
nav_order: 3.5
---

# API
{: .no_toc }

This page describes the BabyBench API for its use in the competition. Details about [MIMo](https://mimo.readthedocs.io/en/latest/), [MuJoCo](https://mujoco.readthedocs.io/en/stable/overview.html), and [Gymnasium](https://gymnasium.farama.org/api/) are not provided here but can be found in their corresponding documentations.  

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Configuration

The list of parameters that can be defined in the configuration files is the following:

- `save_dir` (*float*): The folder where the training logs will be saved. Defaults: `results/test_installation`.
- `behavior` (*float*): The behavior to train. Default: `none`. Options: `none`, `self_touch`, `hand_regard`.
- `scene` (*float*): The scene to use in the environment. Default: `base`. Options: `base`, `crib`, `cubes`.
- `max_episode_steps` (*int*): The maximum number of steps per episode. Default: `1000`.
- `frame_skip` (*int*): The number of physics steps to perform between actions. Default: `1`.
- `render_size` (*int*): The size of the rendered images. Default: `480`.
- `save_logs_every` (*int*): The number of episodes between saving the training logs. Default: `1000`.
- `proprio_velocity` (*bool*): Whether to use the joint velocity in the proprioceptive observation. Default: `True`. 
- `proprio_torque` (*bool*): Whether to use the joint torques in the proprioceptive observation. Default: `True`.
- `proprio_limits` (*bool*): Whether to use the joint limits in the proprioceptive observation. Default: `True`.
- `proprio_actuation` (*bool*): Whether to use the joint actuation in the proprioceptive observation. Default: `True`.
- `vestibular_active` (*bool*): Whether to use the vestibular module. Default: `True`.
- `vision_active` (*bool*): Whether to use the vision module. Default: `True`.
- `vision_resolution` (*int*): The resolution of the vision. Default: `64`.
- `touch_active` (*bool*): Whether to use the touch module. Default: `True`.
- `touch_scale` (*float*): The scale factor for the touch sensors. Default: `1`.
- `touch_function` (*str*): The activation function to use for the touch sensors. Default: `normal`. Options: `normal`, `force_vector`, `force_vector_global`.
- `touch_response` (*str*): The spread response to use for the touch sensors. Default: `nearest`. Options: `nearest`, `spread_linear`. 
- `touch_hands` (*bool*): Whether to use the touch sensors of the hands. Default: `True`.
- `touch_fingers` (*bool*): Whether to use the touch sensors of the fingers. Default: `True`.
- `touch_arms` (*bool*): Whether to use the touch sensors of the arms. Default: `True`.
- `touch_feet` (*bool*): Whether to use the touch sensors of the feet. Default: `True`.
- `touch_legs` (*bool*): Whether to use the touch sensors of the legs. Default: `True`.
- `touch_body` (*bool*): Whether to use the touch sensors of the body. Default: `True`.
- `touch_head` (*bool*): Whether to use the touch sensors of the head. Default: `True`.
- `touch_eyes` (*bool*): Whether to use the touch sensors of the eyes. Default: `False`.
- `actuation_model` (*str*): The actuation model to use. Default: `spring_damper`. Options: `spring_damper`, `muscle`, `positional`.
- `act_hands` (*bool*): Whether to use the actuation of the hands. Default: `True`.
- `act_fingers` (*bool*): Whether to use the actuation of the fingers. Default: `True`.
- `act_arms` (*bool*): Whether to use the actuation of the arms. Default: `True`.
- `act_feet` (*bool*): Whether to use the actuation of the feet. Default: `True`.
- `act_legs` (*bool*): Whether to use the actuation of the legs. Default: `True`.
- `act_body` (*bool*): Whether to use the actuation of the body. Default: `True`.
- `act_head` (*bool*): Whether to use the actuation of the head. Default: `True`.
- `act_eyes` (*bool*): Whether to use the actuation of the eyes. Default: `True`.
- `lock_hands` (*bool*): Whether to lock the position of the hands. Default: `False`.
- `lock_fingers` (*bool*): Whether to lock the position of the fingers. Default: `False`.
- `lock_arms` (*bool*): Whether to lock the position of the arms. Default: `False`.
- `lock_feet` (*bool*): Whether to lock the position of the feet. Default: `False`.
- `lock_legs` (*bool*): Whether to lock the position of the legs. Default: `False`.
- `lock_body` (*bool*): Whether to lock the position of the body. Default: `False`.
- `lock_head` (*bool*): Whether to lock the position of the head. Default: `False`.
- `lock_eyes` (*bool*): Whether to lock the position of the eyes. Default: `False`.

## Initialization

The environment initialization is handled by the ``make_env`` function in the ``babybench.utils`` module:

```python
env = babybench.utils.make_env(config, training=True)
```

``config`` is a dictionary with the configuration parameters detailed above. The ``training`` flag is used to determine whether the environment is being used for training (default) or evaluation. Having ``training=True`` will create or override the training logs in the ``save_dir`` folder and the `scene.xml` file..

The configuration file is read by BabyBench's XML builder (``babybench/build_xml.py``) to create the corresponding `scene.xml` file loaded in the MIMo environment. This also stores a copy of the scene file in the ``save_dir`` folder. The XML file will include the following:
- The config file (commented)
- MIMo's version (v1 with mitten-like hands, v2 with fingers), which depends on the ``behavior`` parameter,
- MIMo's initial location and orientation, which depends on the ``scene`` parameter,
- MIMo's actuation model and the corresponding actuated body parts,
- The scene (``crib`` or ``cubes``; the ``base`` scene is always loaded).

The other environment parameters are passed directly to MIMo's environment creator during the initialization: ``max_episode_steps``, ``frame_skip``, ``render_size``, and ``save_logs_every``. 

## Scenes

### Base

The `base` scene is always loaded. It determined the main physical and rendering configuration. In particular it sets the timestep duration to `0.005` seconds, which is the default value for MIMo, and other MuJoCo solver parameters to the following:
- `iterations="50"`,
- `tolerance="1e-10"`,
- `solver="Newton"`,
- `jacobian="dense"`,
- `cone="elliptic"`,
- `impratio="1.0"`.

In terms of the rendering, the `base` scene creates a gray textured floor and a teal rug with a radius of 1 meter, both of which are under a transparent floor plane and only included for aesthetic purposes. There is also a light gray sky. Shadows are disabled for faster rendering. 5 lights are created, one 5 meters high and 4 on each top corner of a `2x2x2` cube. There are 5 cameras, called `corner`, `top`, `side1`, `side2`, and `closeup`. 

In the ``base`` scene, MIMo is fully free to move.

### Crib

The `crib` scene loads a crib with a mattress, on top of which MIMo is placed. The crib and mattress are fixed and cannot be moved. MIMo's ``lower_body`` is fixed to the mattress of the crib, meaning that he can move his limbs, head, and torso, but he cannot leave his position. MIMo cannot reach the rails of the crib with his hands or feet. The `friction`parameters of the mattress are reduced to 1/10 of the default MuJoCo friction values. Touches with the mattress are still registered, but the contact forces are reduced.

### Cubes

The ``cubes`` scene loads some colorful cubes and balls distributed around MIMo. All these objects have free joints, so they can be picked up and moved. MIMo's body is fixed to the ground, and the angles `hip_bend1`, `hip_lean1`, `hip_rot1`, `hip_bend2`, `hip_lean2`, `hip_rot2`, `head_tilt`, `head_tilt_side`, `right_hip1`, `right_hip2`, `right_hip3`, `right_knee`, `left_hip1`, `left_hip2`, `left_hip3` and `left_knee` are all locked to fixed values such that MIMo is always sitting. He can move his arms and hands, he can rotate his head, and he can move his eyes. From his sitting position, MIMo can reach some of the cubes and balls with his hands.

## Environments

The BabyBench environments use the [Gymnasium](https://gymnasium.farama.org/api/) API. After initializing the environment, users can reset the environment using the ``env.reset()`` method, which returns the observation and information dictionaries. To perform an action, users can use the ``env.step(action)`` method, which takes the action as input and returns the following:
- the observation dictionary, detailed below,
- the reward, which is always 0,
- the terminated flag, which is always ``False``,
- the truncated flag, which is True if the episode reaches the maximum number of steps,
- the information dictionary, which depends on the behavior.

The information dictionary contains, by default, the number of timesteps. Other information is stored depending on the active behavior. 

When using the ``self_touch`` behavior, the information dictionary will return:
- ``steps`` (*int*): the number of steps in the episode,
- ``left_hand_touches`` (*list, int*): the history of body parts touched by the left hand during the episode,
- ``right_hand_touches`` (*list, int*): the history of body parts touched by the right hand during the episode.

Whe using the ``hand_regard`` behavior, the information dictionary will return:
- ``steps`` (*int*): the number of steps in the episode,
- ``right_eye_right_hand`` (*int*): the cumulative number of steps of the episode in which the right hand was in the central field of view of the right eye,
- ``right_eye_left_hand`` (*int*): the cumulative number of steps of the episode in which the left hand was in the central field of view of the right eye,
- ``left_eye_right_hand`` (*int*): the cumulative number of steps of the episode in which the right hand was in the central field of view of the left eye,
- ``left_eye_left_hand`` (*int*): the cumulative number of steps of the episode in which the left hand was in the central field of view of the left eye.

## Sensory observations

MIMo has four sensory modules: proprioception, vestibular system, vision, and touch. These are returned as a dictionary when resetting or stepping the environment. Details of MIMo's sensory modules are provided in [MIMo's documentation](https://mimo.readthedocs.io/en/latest/).

### Proprioception

MIMo's proprioception is accessed as ``obs['observation']``. It contains of a single vector with the concatenation of the following lists:
- the angle of each joint (always active),
- the angular velocity of each joint (if ``proprio_velocity`` is ``True``),
- the torque applied on each torque sensor (if ``proprio_torque`` is ``True``),
- the limits of each joint (if ``proprio_limits`` is ``True``),
- the actuation control of each actuated joint (if ``proprio_actuation`` is ``True``).

The number of joints depends on the model (``47`` for MIMo v1, ``91`` for MIMo v2). The list of joint names is stored in the attribute ``env.proprioception.joint_names``. 

The number of torque sensors depends on the model (``21`` for MIMo v1, ``53`` for MIMo v2). Three dimensional torque components are measured for each sensor, making the total torques observation a vector of length ``63`` or ``159``. The list of torque sensor names is stored in the attribute ``env.proprioception.sensors``.

The number of actuated joints depends on the active actuated body parts. The list of the actuated joints is not stored but can be obtained by running the following code:
```python
actuator_names = []
for i in range(env.model.nu):
    actuator_name = env.model.actuator(i).name
    if actuator_name.startswith("act:"):
        actuator_names.append(actuator_name)
```

### Vestibular

MIMo's vestibular observation is accessed as ``obs['vestibular']`` if ``vestibular_active`` is ``True``. It contains a vector with the following values:
- the 3D linear acceleration of MIMo's head,
- the 3D angular velocity of MIMo's head.

### Vision

MIMo's binocular vision observations are accessed as ``obs['eye_left']`` and ``obs['eye_right']`` if ``vision_active`` is ``True``. They contain the RGB images of the left and right eyes, respectively, as arrays with shape ``(vision_resolution, vision_resolution, 3)``, where the resolution is defined in the configuration file, and with integer values between ``0`` and ``255``.

### Touch

MIMo's touch observation is accessed as ``obs['touch']`` if ``touch_active`` is ``True``. It contains a vector with the activation of each touch sensor in MIMo's skin. The total size of the touch vector will depend on the amount of body parts where the touch modality active, as determined in the configuration file. The sensors are uniformly distributed in each geometry primitive of MIMo's body, with a density defined by MIMo's default touch densities and the ``touch_scale`` parameter in the configuration file. Higher values of ``touch_scale`` will result in fewer touch sensors. 

The touch sensors have three supported output functions, defined in the ``touch_function`` parameter in the configuration file:
- ``normal``: outputs the normal contact force as a scalar.
- ``force_vector``: outputs the contact force vector (normal and frictional forces) in the coordinate frame of the geometry of the corresponding touch sensor.
- ``force_vector_global``: Like ``force_vector``, but in the world coordinate frame instead.

The outputs can be spread to nearby sensors in two ways, defined in the ``touch_response`` parameter in the configuration file:
- ``nearest``: directly adds the output to the nearest sensor and neglects neighbors. 
- ``spread_linear``: spreads the force to nearby sensor points, with a linear decay with distance to the contact point. The force drops to 0 at twice the sensor scale. The force per sensor is normalized such that the total force is conserved.

The touch observations of each body part flattened and concatenated into a single vector in ``obs['touch']``. The positions the touch sensors (in each body's relative coordinate frame) are stored in the dictionary ``env.touch.sensor_positions``, where the keys are the ids of the body parts.

## Actuation models

MIMo has access to three actuation models: the spring-damper model, the muscle model, and the positional model, which you can be set in the configuration file with the ``actuation_model`` parameter. All approaches rely on MuJoCo actuators, but the control and computations differ between them. The actuation models are described in detail in [MIMo's documentation](https://mimo.readthedocs.io/en/latest/). For all actuation models, the dimensions of the action space will depend on the number of active actuators.

The list of the actuated joints is not stored but can be obtained by running the following code:
```python
actuator_names = []
for i in range(env.model.nu):
    actuator_name = env.model.actuator(i).name
    if actuator_name.startswith("act:"):
        actuator_names.append(actuator_name)
```

### Spring-damper model

The spring-damper model uses a spring-damper system to model force-length and force-velocity relationships. MIMo's muscles are approximated as torque motors with linear and instantaneous control response. The control range of the actuators is ``[-1, 1]`` by default. The action space is stored in the attribute ``env.action_space``.

### Muscle model

The muscle model is a more realistic, but computationally more expensive, actuation model. It is an adaptation of the model of [Wochner et al. (2022)](https://arxiv.org/abs/2207.03952), with parameters tuned to mimic an infant's muscles. Each actuator is internally modeled as two opposing and independently controlled muscles.  The control range of the actuators is ``[-1, 1]`` by default. The action space is stored in the attribute ``env.action_space``.

### Positional model

The positional model is less realistic but allows users to directly specify the desired joint angles. The control range depends for each actuator and corresponds to its joint movement range. The action space is stored in the attribute ``env.action_space``.

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