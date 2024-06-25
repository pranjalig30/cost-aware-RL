# Cost-Aware A/B Testing Using Reinforcement Learning

## Project Overview

This project conceptualizes a cost-aware A/B testing scenario as a reinforcement learning (RL) problem to optimize clinical trial treatments. It utilizes various RL methods to dynamically adapt treatment assignments based on accumulating evidence, aiming to maximize overall treatment effectiveness while minimizing costs.

## Table of Contents

- [Introduction](#introduction)
- [Problem Formulation](#problem-formulation)
- [RL Methods](#rl-methods)
- [Simulation Environment](#simulation-environment)
- [Results and Conclusion](#results-and-conclusion)
- [Installation](#installation)
- [Usage](#usage)
- [License](#license)

## Introduction
Background

A/B testing (a.k.a. randomized controlled trials, randomized experiments) is one of the most important ways to understand causal relationships. In a typical A/B testing setup, there will be one (or more) treatment group and one control group, and a pool of subjects are randomly assigned to the experimental groups based on pre-determined proportions (e.g., equal assignments). 

While this is a perfectly legitimate way to test causality, it can be inefficient in practice. Imagine a clinical trial of two treatment options: drug A and placebo B, and let's assume that (in fact) drug A is much more effective than placebo B in treating a certain condition. Then, every subject that is assigned to the placebo group has to (unfortunately) endure some non-trivial costs, i.e., their conditions are not treated timely even when an effective drug exists. Note that some of the costs are necessary - after all, we don't know the effectiveness of drug A a priori and need a sufficient number of people in both groups to find out. However, as the effectiveness of drug A becomes clearer and clearer over the course of the experiment, perhaps it makes sense to gradually reduce the assignment to the placebo group, in order to reduce costs. 

This is the basic idea behind **cost-aware A/B testing**. It is an important emerging topic in experimentation, and has attracted a lot of attention from both researchers and practitioners.## Problem Formulation

## Problem Statement
Formally, consider an experiment with $k$ treatment options $\{T_1, \ldots, T_k\}$ (no need to explicitly differentiate between treatment and control in a traditional sense, one of these options could be a control condition). Each of the $k$ treatments has a true underlying treatment effect $\{TE_1, \ldots, TE_k\}$, which is unknown to the experimenter before the experiment is conducted. For an arbitrary subject $i$ that is assigned to a treatment $j$, the realized treatment effect $TE_{ij}$ is a random draw from the normal distribution surrounding the true treatment effect with unknown variance, i.e., $TE_{ij} \sim N(TE_j, \sigma^2_j)$. There are $N$ subjects available in total, who can be assigned to the different treatment groups. The goal of the experimenter is twofold: (1) the experimenter wants to understand the effectiveness of each treatment option (this is why the experiment is conducted in the first place); (2) at the same time, the experimenter wants to be cost-aware in treatment assignment and try to avoid incurring too much costs.

### Agent
The experimenter or algorithm deciding which treatment to assign to each subject.

### Environment
The clinical trial setting, including the pool of subjects and potential outcomes (effects of treatments or placebos). The environment's state is characterized by the current knowledge of treatment effectiveness and the number of subjects treated.

### States

- **Treatment Effectiveness Estimates (ˆTE)**: Estimates of true treatment effects, updated through experimentation.
- **Number of Subjects Remaining (N_remaining)**: Number of subjects yet to be assigned.
- **Cost Information (C)**: Total cost incurred or costs associated with each treatment.

### Actions
Assigning one of the possible treatments, including the control condition (placebo), to a subject in each trial.

### Rewards
The observed effect of the treatment on the subject, higher for more effective treatments. Negative rewards (costs) are associated with assigning subjects to less effective treatments.

### Objective
Maximize overall treatment effectiveness while minimizing costs. The agent aims to quickly identify the most effective treatments and allocate more subjects to these treatments.

## RL Methods

1. **Epsilon Greedy with Bonferroni Correction**
   - Balances exploration and exploitation.
   - Statistically robust with higher placebo counts and significant p-values.
   - Preferred for careful cost consideration and effective allocation of subjects.

2. **Upper Confidence Bound (UCB) Strategy**
   - Balanced approach to exploration.
   - Fewer placebo trials, potentially affecting statistical robustness.

3. **Gradient Method**
   - Heavily favors one treatment.
   - May not be ideal for cost-aware scenarios if treatment superiority is not well-established.

## Simulation Environment
To simulate this environment, the following parameters are set:

- **Treatment Effects (TE_j)**: Manually specify the true average treatment effects for each treatment.
- **Variance (σ_j)^2**: Specify the variance for the treatment effects.
- **Number of Subjects (N)**: Decide how many subjects will be available for the experiment.

## Results and Conclusion
The Epsilon Greedy with Bonferroni correction method stands out for balancing exploration and exploitation while maintaining statistical robustness and cost-awareness. It minimizes unnecessary placebo assignments and supports effective treatment allocation, aligning with ethical and economic imperatives in clinical trials.

## Installation

1. Clone the repository:
    ```sh
    git clone https://github.com/pranjalig30/cost-aware-RL/
    cd cost-aware-RL
    ```

2. Install the required dependencies:
    ```sh
    pip install -r requirements.txt
    ```

## Usage

1. Run the Jupyter Notebook:
    ```sh
    jupyter notebook
    ```
2. Open `Assignment 2 - Cost-Aware AB Testing.ipynb` and run the cells to see the simulation results and analyses.
---

Feel free to customize any sections to better fit your project details or personal preferences.
