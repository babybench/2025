---
title: Competition guidelines
layout: default
nav_order: 5
---

# Competition guidelines
{: .no_toc }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Evaluation committee

The evaluations will be conducted by a committee of experts in the field of robotics, machine learning, and developmental psychology, invited by the organizers of the competition. The review will be a single-blind process. The experts will [score](#scoring) the submissions and be encouraged to provide constructive feedback to the authors of the submissions. The final decisions on the winners will be made on the basis of the aggregated scores of all the experts.



## Scoring

Each submission will be scored out of 10 points, based on four criteria, described in detail below. These criteria reflect both the scientific goals of the competition and the broader aims of the IEEE ICDL community. They are intended to reward not only performance but also developmental relevance, interpretability, and methodological soundness.

A minimum score of 1 point in each of the first three criteria (likeness, achievement, plausibility) will be required to win the competition.

**Note**: The evaluation criteria are subject to change as the competition progresses. We will update this page with the final criteria as soon as they are finalized.

### Likeness of the generated examples (3 points)

The first criterion focuses on how closely the learned behaviors match the expected behaviors. The judges will evaluate videos and logs from 10 episodes with random initial conditions. The evaluation will consider qualitative features, including body trajectories, variability across trials, and resemblance to real infants.

The likeness score will be subjective for each judge. However, authors are encouraged to take a look at the [example videos](about/#behaviors) to get a sense of what the expected behaviors should look like. 

### Achievement of the target behavior (3 points)

Submissions will be evaluated on how well they replicate the learning of the target behavior. The evaluation will be made on the basis of the training logs generated during the training process and any results reported by the authors in the extended abstract.

Running the [evaluation code](submission/#evaluation) will return a preliminary score based on:

- the fraction of body parts touched by each hand for the self-touch task,

- the fraction of timesteps with either hand in the field of view of each eye for the hand-regard task.

This preliminary score is only provided as a refernce for the authors to assess their model's performance, and *will not necessarily reflect the final score given by the judges*.

Incomplete or inconsistent results that nonetheless show promise will be rewarded in spite of the lack of completeness. This criterion is intended to encourage models that are both effective and relevant to the task at hand.

### Plausibility of the learning mechanism (3 points)

One of the central aims of BabyBench is to promote the exploration of learning processes that are not only effective but also cognitively and developmentally plausible. This criterion rewards submissions that are inspired by mechanisms such as curiosity, intrinsic motivation, predictive coding, or self-supervised representation learning.

The plausibility score will be based on the description of the method provided in the extended abstract and potentially on the logs generated during the training process. The judges will be encouraged to favor models that reflect general principles from developmental psychology or neuroscience, or that offer interpretable insights into learning dynamics beyond the specific task at hand.

### Computational efficiency (1 bonus point)

Although not a primary evaluation criterion, computational efficiency will be considered as a potential bonus point, particularly in the case of ties. The bonus point may be awarded to models that achieve strong results while remaining lightweight in terms of:

- total training time,

- simulation speed,

- memory usage,

- or hardware demands.

The goal of this criterion is to encourage solutions that are elegant and accessible, without requiring extensive computational resources. This criterion will be adjusted based on the number of participants and the complexity of each task. We encourage submissions that rely on plausible learning mechanisms that can be run in a reasonable amount of time and memory.



## Prizes

The winning team of the BabyBench Competition will receive a **€150 prize, generously sponsored by the IEEE Computational Intelligence Society**. In addition to the monetary award, the winning team will be invited to **present their submission during the IEEE ICDL conference**, offering an opportunity to share their work with a broad interdisciplinary audience.

Finalist teams who make it to the final evaluation round will receive honorable mentions in recognition of their contributions. These mentions will be announced during the competition session and highlighted in official competition materials.

Our goal is to celebrate creativity, rigor, and developmental insight—whether you win, place, or simply participate, your work helps advance the conversation. We look forward to seeing your innovative approaches and the impact they will have on our understanding of infant learning and development.



## Rules

The BabyBench Competition aims to bring together researchers and students in the fields of robotics, machine learning, developmental psychology, and beyond. We welcome participants from all backgrounds, institutions, and levels of experience. There are no excluding criteria for participation—collaboration across disciplines and perspectives is strongly encouraged.

While the competition is open and inclusive by design, we strongly encourage submissions that align with the spirit of ICDL. This means a focus on modeling, understanding, or replicating infant learning and behavior through mechanisms that are plausible, interpretable, or relevant to developmental processes. We are particularly interested in approaches that bridge the gap between artificial and biological learning systems, drawing insights from cognitive development, neuroscience, and behavioral science.

Submissions may employ any modeling framework or data modality, but should aim to contribute meaningfully to our understanding of how learning unfolds in early development—whether through simulation, robotics, theoretical modeling, or analysis of behavioral data. We encourage submissions that are reproducible, open-source, and accessible to the broader research community.

To keep the competition simple, we do not require submissions to include the full code used to learn the behaviors. Only the winning team will be expected to provide the code, which will be tested as a verification check before the announcement.

