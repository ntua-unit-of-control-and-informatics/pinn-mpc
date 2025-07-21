# pinn-mpc
Code to accompany the research on: "An Explicit Model Predictive Control Framework Based On Physics-Informed Neural Networks."

## Table of Contents
- [Overview](#overview)
- [Code](#code)
- [How to Run Code](#how-to-run-code)
- [Prerequisites](#prerequisites)
- [License](#license)

## Overview

This repository contains the Python Notebook developed as part of the research titled **"An Explicit Model Predictive Control Framework Based On Physics-Informed Neural Networks."** by Argyri Kardamaki, Teo Protoulis, Alex Alexandridis and Haralambos Sarimveis. We implement a **Physics-Informed Neural Network (PINN)** to approximate the explicit solution of a nonlinear **Model Predictive Control (MPC)** problem. The controller learns the closed-loop dynamics and optimization policy offline, by training on simulated trajectories while embedding the system's physics directly into the loss function.

The **PINN-MPC** controller produces state and control trajectories by minimizing a composite loss that includes:
- **Physics residuals** from the system's differential equation,
- **Tracking errors** to a given set-point and solution,
- **Initial Condition** enforcement to state and,
- **Soft bounds** on the control input and state.

The case study for the PINN-MPC is a classic nonlinear water tank system. The controller is trained offline to learn optimal trajectories that track a desired set-point while satisfying the underlying system dynamics and constraints.

## Code

All functionality is provided in the notebook: `PINN_MPC_Github_Code.ipynb`
The notebook includes clearly separated code blocks for:

- **Training** the PINN-MPC using a two-phase Adam optimizer with configurable hyperparameters.
- **Validation** of the trained controller on hundreds of set-point and disturbance scenarios.

Each section includes all relevant functions and is self-contained for experimentation.
Users are encouraged to modify the parameters (e.g., loss weights, batch size, number of epochs, learning rates, prediction horizon) to experiment with different control behaviors or system settings.

## How to Run Code

1. Open the notebook `PINN_MPC_Github_Code.ipynb` in Jupyter or Colab.
2. Run all cells to:
   - Train the PINN-MPC on synthetic trajectory data,
   - Evaluate it on challenging test scenarios,
   - Visualize performance plots.
3. Adjust training or simulation parameters in the respective sections to explore different controller configurations.

**Performance Tip**: Users are encouraged to **run the code on a GPU** to significantly reduce training time. To run your notebook on a local GPU with Google Colab, see Official Colab guidance:  https://research.google.com/colaboratory/local-runtimes.html

## Prerequisites

This notebook requires **Python 3.8+** and the following Python packages:

- `torch` (PyTorch ≥ 2.0)
- `numpy`
- `matplotlib`
- `scipy`

## License

This project is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License- see the [LICENSE](LICENSE-CC-BY-NC.txt) file for details.
