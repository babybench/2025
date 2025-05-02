---
title: About
layout: default
nav_order: 1
---

# About
{: .no_toc }

BabyBench is a multimodal benchmark of infant behaviors for developmental artificial intelligence. The BabyBench Competition hosted at IEEE ICDL invites participants to model infant-like learning in simulated environments using MIMo, the multimodal infant model. 

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Motivation

How do infants develop a sense of self?

The early stages of human development are characterized by rich sensorimotor exploration where infants engage in self-touch, self-reach and spontaneous movements that contribute to body awareness and motor control (Rochat, 1998). These behaviors are observed within the first months of life and are fundamental for the emergence of calibrated proprioception and motor coordination. While infant development has been extensively studied in psychology and neuroscience, replicating these behaviors on humanoid robotic platforms remains a major challenge.

This challenge invites participants to design and implement mechanisms that enable MIMo, a baby-sized humanoid agent equipped with a tactile skin and binocular vision, to autonomously generate **self-touching** and **hand regard** behaviors similar to those seen in human infants. The objective here is to model developmental principles such as learning how to explore, building and exploiting sensorimotor loops and intrinsic motivation that drives actions in human infants (Oudeyer & Smith, 2016). Participants will work within custom-designed MIMo environments. Successful solutions should demonstrate emergent behaviors where the agent discovers, through self-exploration, affordances of movements and refines motor skills without explicitly programmed trajectories.

Our aim is to encourage researchers from diverse backgrounds to contribute to the field of developmental artificial intelligence by developing innovative solutions to this challenging problem. We hope that this project will provide a unique opportunity to explore the intersection of machine learning, robotics, and developmental psychology.

#### Recommended reading
{: .no_toc }

- Rochat, 1998: [Self-perception and action in infancy](https://idp.springer.com/authorize/casa?redirect_uri=https://link.springer.com/article/10.1007/s002210050550&casa_token=qvuUDsPAEpMAAAAA:QemJo9z91V2U6qtErioDuNJhPcErVSCAW54GTC_AqIukxX0R2I3ap8dI3mUHD2ffI9YrmHWxMYjXB2hiRiY)
- Oudeyer and Smith, 2016: [How evolution may work through curiosity‐driven developmental process](https://onlinelibrary.wiley.com/doi/pdfdirect/10.1111/tops.12196)


## Behaviors

The first BabyBench Competition focuses on two early behaviors that demonstrate the emergence of a sense of self in infant development: self-touch and hand regard. These behaviors are not only central to how infants begin to build sensorimotor representations of their own bodies, but also serve as a foundation for more complex cognitive and social capabilities. 

### Self-touch

Self-touch behaviors emerge within the first weeks of life and are a crucial form of sensorimotor exploration. Infants frequently touch their face, torso, and limbs, gradually refining their ability to reach and coordinate across the body.

<iframe width="480" height="320" src="../static/videos/selftouch_target.mp4" frameborder="0" allowfullscreen></iframe>

#### Behavioral insights
{: .no_toc }

Self-touch supports the development of body awareness, spatial proprioception, and the formation of a body schema – an internal model of one’s own body. Even in utero, fetuses demonstrate purposeful self-touch, suggesting an early developmental drive for self-directed exploration. Self-touch exploration is not random, but rather evolves throughout development, with infants gradually covering more of their body surface (Khoury et al., 2022).

#### Ideas to explore
{: .no_toc }

Tactile feedback from the skin, combined with proprioceptive and motor signals, can help infants learn the consequences of their own movements. The development of a body schema can be facilitated through self-generated haptic goals, i.e. the expectation of perceiving a touch on a given body part, which can serve as a goal for self-reach (Marcel et al., 2022).  

#### Recommended reading
{: .no_toc }

- Somogyi et al., 2023: [Tactile training facilitates infants' ability to reach to targets on the body](https://srcd.onlinelibrary.wiley.com/doi/pdfdirect/10.1111/cdev.13891)
- Khoury et al., 2022: [Self-touch and other spontaneous behavior patterns in early infancy](https://ieeexplore.ieee.org/abstract/document/9962203)
- Marcel et al., 2022: [Learning to reach to own body from spontaneous self-touch using a generative model](https://ieeexplore.ieee.org/abstract/document/9962186)

### Hand regard

Typically appearing around 2–3 months of age, hand regard is characterized by infants visually tracking and fixating on their own hands. This behavior marks a shift toward coordinated visual-motor integration.

<iframe width="480" height="320" src="../static/videos/handregard_target.mp4" frameborder="0" allowfullscreen></iframe>

#### Behavioral insights
{: .no_toc }

Hand regard enables infants to link visual and proprioceptive modalities, paving the way for visually guided reaching and object manipulation (Corbetta, 2021). Studies show that infants often engage in extended hand gazing, appearing mesmerized by their own movements (van der Meer, 1997). The behavior is reduced at about 4 months, when infants shift their visual attention to objects as they learn to reach towards them, without the necessity of fixating their own hands.

#### Ideas to explore
{: .no_toc }

Hand regard can lead to redundancies in the visual and proprioceptive sensory modalities, resulting in observations that are easier to encode (López et al., 2023). This behavior may also support the development of internal forward models, allowing infants to anticipate the outcomes of self-initiated actions. 

#### Recommended reading
{: .no_toc }


- van der Meer, 1997: [Keeping the arm in the limelight: Advanced visual control of arm movements in neonates](https://www.sciencedirect.com/science/article/abs/pii/S1090379897800402)
- Corbetta, 2021: [Perception, action, and intrinsic motivation in infants' motor-skill development](https://journals.sagepub.com/doi/abs/10.1177/09637214211031939)
- Homma, 2018: [Hand Recognition Obtained by Simulation of Hand Regard](https://www.frontiersin.org/journals/psychology/articles/10.3389/fpsyg.2018.00729/full)
- López et al., 2023: [Eye-Hand Coordination Develops from Active Multimodal Compression](https://ieeexplore.ieee.org/abstract/document/10364414)
- Wijesinghe et al., 2018: [Robot End Effector Tracking Using Predictive Multisensory Integration](https://www.frontiersin.org/journals/neurorobotics/articles/10.3389/fnbot.2018.00066/full)

## Modeling

The BabyBench Competition invites participants to model behavior learning using a wide range of approaches. While there are no restrictions to the types of algorithms or architectures that can be used, we strongly encourage submissions that rely on biologically plausible and computationally interpretable approaches, including unsupervised, self-supervised, and reinforcement learning. In particular, models that draw inspiration from the fields of intrinsic motivations, open-ended learning, and other developmentally inspired approaches will be highly valued. Learning plausibility is one of the [evaluated criteria](../competition/#plausibility-of-the-learning-mechanism-3-points) for submissions. Next, we provide a brief overview of some of these modeling approaches and how they relate to the BabyBench competition.

### Reinforcement learning

Reinforcement learning (RL) is one of the main branches of machine learning, inspired by how humans and animals learn through trail-and-error. RL agents learn from feedback they receive when interacting with their environments, which can be in the form of rewards or punishments. Over time, an agent will refine its behavior to maximize the cumulative rewards it receives. This framework is particularly well suited for learning behaviors in complex and dynamic environments like the ones of the BabyBench competition. However, BabyBench presents an important challenge for RL methods: the environments do not provide any explicit feedback (extrinsic rewards), and thus the agents need to learn autonomously.

One of the central challenges in reinforcement learning is the balance between exploration—trying new things—and exploitation—leveraging known strategies to maximize reward. Too much exploitation leads to stagnation, while too much exploration can be inefficient. Intrinsic motivations help agents explore more wisely, especially when external feedback is limited or nonexistent.

#### Recommended reading
{: .no_toc }

- Sutton and Barto, 2015: [Reinforcement Learning: An Introduction](https://web.stanford.edu/class/psych209/Readings/SuttonBartoIPRLBook2ndEd.pdf)

### Intrinsic motivations

Intrinsic motivations introduce a more self-driven approach to learning. Inspired by human curiosity, intrinsically motivated agents seek out novelty, surprise, learning progress, or autonomously calibrated skills. This helps them explore more broadly and develop general-purpose skills, even in the absence of extrinsic rewards. For example, curiosity-driven learning is a specific form of intrinsic motivation where an agent seeks out situations that yield new or unexpected information. Like a child poking around to see what happens, a curious agent explores the world not because it has to, but because it wants to reduce uncertainty or discover something novel.

#### Recommended reading
{: .no_toc }

- Pathak et al., 2017: [Curiosity-driven Exploration by Self-supervised Prediction](https://arxiv.org/abs/1705.05363)
- Yu et al., 2019: [Unsupervised Visuomotor Control through Distributional Planning Networks](https://arxiv.org/abs/1902.05542)
- Aubret et al., 2023: [ An Information-Theoretic Perspective on Intrinsic Motivation in Reinforcement Learning: A Survey ](https://www.mdpi.com/1099-4300/25/2/327)

### Open-ended learning

Open-ended learning describes the ability of a system to continually develop new skills and behaviors without a predefined objective. Rather than being trained for one specific task, an open-ended learner grows over time by building on previous experiences and seeking out new challenges. One common approach for open-ended learning is to achieve self-generated goals, where the agent sets its own objectives and strives to achieve them. It enables more directed behavior and can help guide exploration in meaningful ways. By learning how to attain different goals, agents can develop a flexible understanding of their environment, enabling them to generalize and adapt to future tasks more efficiently.

#### Recommended reading
{: .no_toc }

- Nair et al., 2018: [Visual Reinforcement Learning with Imagined Goals](https://arxiv.org/abs/1807.04742)
- Florensa et al., 2017: [Automatic Goal Generation for Reinforcement Learning Agents](https://arxiv.org/abs/1705.06366)
- Cartoni et al., 2023: [REAL-X—Robot Open-Ended Autonomous Learning Architecture: Building Truly End-to-End Sensorimotor Autonomous Learning Systems](https://ieeexplore.ieee.org/iel7/7274989/10360134/10132490.pdf)




### Other developmentally-inspired approaches

Developmental learning takes inspiration from how human infants acquire knowledge and skills over time. Instead of jumping straight into complex tasks, a developmental learner progresses through stages, mastering simpler behaviors first and gradually tackling more complex ones. This scaffolding approach can lead to more robust and transferable learning, and is central to building truly adaptive, long-term learning systems.

**Curriculum learning** involves organizing training experiences in a meaningful sequence—starting with easier tasks and gradually increasing difficulty. Much like a school curriculum, this approach helps learning agents build a strong foundation before facing more challenging problems. When aligned with intrinsic motivation or open-ended goals, it can foster more efficient and stable learning.

**Empowerment** is a lesser-known but powerful concept in intrinsic motivation. It refers to an agent’s drive to place itself in states where it has many options and a high degree of control over the future. In essence, an empowered agent seeks to remain capable and influential—choosing situations where it can make a difference. 

#### Recommended reading
{: .no_toc }

- Narvekar et al., 2020: [Curriculum Learning for Reinforcement Learning Domains: A Framework and Survey](https://arxiv.org/pdf/2003.04960)
- Salge et al., 2014: [Changing the Environment Based on Empowerment as Intrinsic Motivation](https://www.mdpi.com/1099-4300/16/5/2789)

## MIMo

MIMo is a multimodal infant model built on top of the MuJoCo simulation platform that can be run using Gymnasium environments. His body is composed of simple geometrical primitives adjusted to match the dimensions of an average 18-month-old child. Two different versions of MIMo are available: one with mitten-like hands, that has 44 degrees of freedom,  and a computationally more expensive one with five-fingered hands and a total of 88 degrees of freedom. 

MIMo has access to four sensory modalities: proprioception, vestibular system, vision, and touch. Proprioceptive observations contain the position, velocity, force and limit values for each joint in MIMo's body. He has binocular vision from cameras located in his eyes, which render RGB images with a resolution and field-of-view defined by the user. Touch perception is implemented as a full-body virtual skin with uniformly distributed MuJoCo haptic sensors with densities defined per body part, allowing for higher density in the hands and fingers, and registering contacts with objects or other parts of MIMo's body.

MIMo can move using three different types of actuation models: positional controllers that directly select the angle of each joint, torque controllers where actions are modeled as a motor with a spring-damper system, and muscle controllers where joints are actuated by differentially activating antagonistic muscle pairs.

A full description of MIMo's sensory and actuation modules used in BabyBench can be found in the [API](../api) page. You can download and use MIMo for your own experiments [here](https://github.com/trieschlab/MIMo). To know more, read the MIMo [documentation](https://mimo.readthedocs.io/en/latest/).

#### Recommended reading
{: .no_toc }

- Mattern et al., 2024: [MIMo: A Multimodal Infant Model for Studying Cognitive Development](https://arxiv.org/pdf/2312.04318)
- Todorov et al., 2012: [MuJoCo: A physics engine for model-based control](https://ieeexplore.ieee.org/abstract/document/6386109/)

---

### [Next page: Installation](../installation)
{: .no_toc }