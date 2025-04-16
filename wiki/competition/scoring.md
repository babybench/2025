---
title: Scoring system
layout: default
parent: Competition guidelines
nav_order : 2
---


# Scoring
{: .no_toc }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

Each submission will be scored out of 10 points, based on four criteria, described in detail below. These criteria reflect both the scientific goals of the competition and the broader aims of the IEEE ICDL community. They are intended to reward not only performance but also developmental relevance, interpretability, and methodological soundness.

A minimum score of 1 point in each of the first three criteria (likeness, achievement, plausibility) will be required to win the competition. 

**Note**: The evaluation criteria are subject to change as the competition progresses. We will update this page with the final criteria as soon as they are finalized.

## Likeness of the generated examples (3 points)

The first criterion focuses on how closely the learned behaviors match the expected behaviors. The judges will evaluate videos and logs from 10 episodes with random initial conditions. The evaluation will consider qualitative features, including body trajectories, variability across trials, and resemblance to real infants. 

The likeness score will be subjective for each judge. However, authors are encouraged to take a look at the [example videos](../about/behaviors.md) to get a sense of what the expected behaviors should look like.

## Achievement of the target behavior (3 points)

Submissions will be evaluated on how well they replicate the learning of the target behavior. The evaluation will be made on the basis of the training logs generated during the training process and any results reported by the authors in the extended abstract.

Running the [evaluation code](../submission/evaluation) will return a preliminary score based on:
- the fraction of body parts touched by each hand for the self-touch task,
- the fraction of timesteps with either hand in the field of view of each eye for the hand-regard task.

This preliminary score is only provided as a refernce for the authors to assess their model's performance, and *will not necessarily reflect the final score given by the judges*. 

Incomplete or inconsistent results that nonetheless show promise will be rewarded in spite of the lack of completeness. This criterion is intended to encourage models that are both effective and relevant to the task at hand.

## Plausibility of the learning mechanism (3 points)

One of the central aims of BabyBench is to promote the exploration of learning processes that are not only effective but also cognitively and developmentally plausible. This criterion rewards submissions that are inspired by mechanisms such as curiosity, intrinsic motivation, predictive coding, or self-supervised representation learning. 

The plausibility score will be based on the description of the method provided in the extended abstract and potentially on the logs generated during the training process. The judges will be encouraged to favor models that reflect general principles from developmental psychology or neuroscience, or that offer interpretable insights into learning dynamics beyond the specific task at hand.

## Computational efficiency (1 bonus point)

Although not a primary evaluation criterion, computational efficiency will be considered as a potential bonus point, particularly in the case of ties. The bonus point may be awarded to models that achieve strong results while remaining lightweight in terms of:
- total training time,
- simulation speed,
- memory usage,
- or hardware demands.

The goal of this criterion is to encourage solutions that are elegant and accessible, without requiring extensive computational resources. This criterion will be adjusted based on the number of participants and the complexity of each task. We encourage submissions that rely on plausible learning mechanisms that can be run in a reasonable amount of time and memory.