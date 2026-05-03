# PINN for a Mass-Spring System

A learning-oriented implementation of a **Physics-Informed Neural Network (PINN)** for a simple mass-spring oscillator.

This repository was built as a study project to understand the basic idea of PINNs by comparing:

- a **purely data-driven neural network**
- a **physics-informed neural network** that additionally enforces the governing ODE

The example problem is a 1D mass-spring system with displacement data generated from an analytical solution.

---

## Motivation

I studied this project to understand how physical constraints can be incorporated into neural network training, especially in cases where data are limited or noisy.

This repository is **inspired by** the example project below:

- [bentaps/PINN-example](https://github.com/bentaps/PINN-example)

However, this repository should be understood as a **personal learning and reconstruction project**.  
I read and followed the core idea of the reference example, then reorganized the problem in a way that matched my current level of understanding:

- using a simple mass-spring system as the target problem
- explicitly comparing a standard neural network with a PINN
- tracing how the physics residual changes the training objective
- using the notebook as a self-study record rather than a workshop handout

---

## Problem Setup

The target system is a 1D undamped mass-spring oscillator:

\[
m\ddot{x} + kx = 0
\]

where:

- \(m\) is the mass
- \(k\) is the spring constant
- \(x(t)\) is the displacement

The notebook generates:

- a small noisy training set
- a dense test set based on the analytical solution

The goal is to compare:

1. a neural network trained only on data
2. a PINN trained on both data loss and physics loss

---

## What Is in This Repository

- `mass_spring_system_solutions.ipynb`
  - main notebook
  - data generation
  - baseline neural network training
  - PINN training
  - result visualization

- `PINN.pdf`
  - supporting presentation/material used while studying the topic

- `PINN.pptx`
  - presentation version of the same topic

- `2302.04107v1.pdf`, `2304.14374v3.pdf`
  - reference papers collected during study

---

## Method

### 1. Purely data-driven model

A feedforward neural network is trained only to minimize mean squared error between:

- predicted displacement
- noisy observed displacement

This serves as the baseline.

### 2. Physics-informed model

The PINN uses the same network structure, but adds a physics residual term to the loss.

The residual is constructed from:

\[
m\ddot{x} + kx
\]

using automatic differentiation in PyTorch.

So the loss contains:

- **data loss**
- **physics loss**

This makes the model learn not only from sparse observations, but also from the governing equation.

---

## What I Learned from This Project

This project helped me understand:

- how PINNs differ from ordinary regression models
- how automatic differentiation can be used to construct physics residuals
- why physics constraints can improve learning when data are sparse
- how to structure a simple PINN experiment from scratch in PyTorch

More importantly, it helped me move from *“I know the concept of PINNs”* to *“I can explain and implement the basic workflow myself.”*

---

## Current Scope and Limitations

This repository is intentionally simple and should be interpreted as a **learning-scale prototype**, not a full research-grade PINN framework.

Current limitations include:

- only a simple 1D oscillator problem is considered
- the notebook focuses on concept demonstration rather than extensive benchmarking
- hyperparameter exploration is limited
- the code is notebook-centered rather than packaged as a reusable library

---

## How to Run

1. Open `mass_spring_system_solutions.ipynb`
2. Install the required packages
3. Run the notebook from top to bottom

If needed, install dependencies with:

```bash
pip install -r requirements.txt
```

---

## Requirements

The notebook uses:

- `torch`
- `numpy`
- `matplotlib`

See `requirements.txt` for a minimal environment.

---

## Acknowledgment

This repository is based on concepts and learning structure inspired by:

- [bentaps/PINN-example](https://github.com/bentaps/PINN-example)

The goal here is not to present the idea as entirely original, but to document my own understanding and reconstruction of the method through a smaller personal study project.
