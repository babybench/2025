---
title: About
layout: default
nav_order: 1
---

# About
{: .no_toc }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Motivation

How do infants develop a sense of self?

The early stages of human development are characterized by rich sensorimotor exploration where infants engage in self-touch, self-reach and spontanoous movements that contribute to body awareness and motor control (Rochat, 1998). These behaviors are observed within the first months of life and are fundamental for the emergence of the calibration of proprioception and motor coordination. While infant development has been extensively studied in psychology and neuroscience, replicating these behaviors on a humanoid robotic platform remains a major challenge.

This challenge invites participants to design and implement mechanisms that enable MIMo, a baby-sized humanoid agent equipped with a tactile skin and binocular vision, to autonomously generate self-touching and hand regard behaviors similar to those seen in human infants. The objective here is to model developmental principles such as learning how to explore, building and exploiting sensorimotor loops and intrinsic motivation that drives actions in human infants (Oudeyer & Smith, 2016). Participants will work within custom-designed MIMo environments, specifically tailored to support the study of . Successful solutions should demonstrate emergent behaviors where the agent discovers, through self-exploration, affordances of movements and refines motor skills without explicitly programmed trajectories.  

Our aim is to encourage researchers from diverse backgrounds to contribute to the field of developmental artificial intelligence by developing innovative solutions to this challenging problem. We hope that this project will provide a unique opportunity to explore the intersection of machine learning, robotics, and developmental psychology.

## Behaviors

The first BabyBench Competition focuses on two early behaviors that demonstrate the emergence of a sense of self in infant development: self-touch and hand regard. These behaviors are not only central to how infants begin to build sensorimotor representations of their own bodies, but also serve as a foundation for more complex cognitive and social capabilities. 

### Self-touch

Self-touch behaviors emerge within the first weeks of life and are a crucial form of sensorimotor exploration. Infants frequently touch their face, torso, and limbs, gradually refining their ability to reach and coordinate across the body.

* Behavioral insights: Self-touch supports the development of body awareness, spatial proprioception, and the formation of a body schema – an internal model of one’s own body. Even in utero, fetuses demonstrate purposeful self-touch, suggesting an early developmental drive for self-directed exploration. Self-touch exploration is not random, but rather evolves throughout development, with infants gradually covering more of their body surface (Khoury et al., 2022).

* Ideas to explore: Tactile feedback from the skin, combined with proprioceptive and motor signals, can help infants learn the consequences of their own movements. The development of a body schema can be facilitated through self-generated haptic goals, i.e. the expectation of perceiving a touch on a given body part, which can serve as a goal for self-reach (Marcel et al., 2022). 

### Hand regard

Typically appearing around 2–3 months of age, hand regard is characterized by infants visually tracking and fixating on their own hands. This behavior marks a shift toward coordinated visual-motor integration.

* Behavioral insights: Hand regard enables infants to link visual and proprioceptive modalities, paving the way for visually guided reaching and object manipulation. Studies show that infants often engage in extended hand gazing, appearing mesmerized by their own movements.

* Ideas to explore: Hand regard can lead to redundancies in the visual and proprioceptive modalities, resulting in sensory states that are easier to encode (López et al., 2023). This behavior may also support the development of internal forward models, allowing infants to anticipate the outcomes of self-initiated actions.

## MIMo

BabyBench is built on top of MIMo, a multimodal infant model that leverages the MuJoCo simulation engine and the Gymnasium framework. You can download and use MIMo for your own experiments [here](https://github.com/trieschlab/MIMo). To know more, read the MIMo [documentation](https://mimo.readthedocs.io/en/latest/).