# pinn-mpc
Code to accompany the research on: **"An Explicit Model Predictive Control Framework Based On Physics-Informed Neural Networks."**

## Table of Contents
- [Overview](#overview)
- [Code](#code)
- [How to Run Code](#how-to-run-code)
- [Prerequisites](#prerequisites)
- [License](#license)

## Overview
This repository contains the Python notebooks developed as part of the research titled **"An Explicit Model Predictive Control Framework Based On Physics-Informed Neural Networks."** by Argyri Kardamaki, Teo Protoulis, Alex Alexandridis and Haralambos Sarimveis.

We implement **Physics-Informed Neural Networks (PINNs)** to approximate the explicit solution of nonlinear **Model Predictive Control (MPC)** problems. The controllers learn closed-loop behavior offline by training on simulated trajectories while embedding system physics directly into the loss function.

The **PINN-MPC** framework minimizes a composite loss consisting of:
- **Physics residuals** from the system dynamics,
- **Tracking errors** toward a set-point trajectory,
- **Initial-condition consistency**, and
- **Soft constraints** on states and control inputs.

The repository includes implementations for both:
- **SISO** nonlinear water-tank system
- **MIMO** nonlinear benchmark system used in the research study

Both controllers are trained offline and evaluated through extensive closed-loop simulations.

## Code
Two notebooks are provided:

- `PINN_MPC_SISO_Github_Code.ipynb` – full SISO PINN-MPC training, validation metrics, and closed-loop plots.
- `PINN_MPC_MIMO_Github_Code.ipynb` – full MIMO PINN-MPC training, validation, and closed-loop performance.

The code includes clearly separated sections for:
- **Training** using a two-phase Adam optimizer;
- **Validation & metrics** on test scenarios;
- **Closed-loop simulations** with performance plots.

The MIMO training dataset is split into three files for GitHub compatibility:
- `mimo_training_samples_x.pt` – initial states (`x0_all`)
- `mimo_training_samples_ysp.pt` – set-points (`ysp_all`)
- `mimo_training_samples_ud.pt` – inputs, disturbances, and metadata (`u0_all`, `d0_all`, `meta`)

Test datasets are also included for both SISO and MIMO systems.

Users may freely adjust hyperparameters (loss weights, batch size, learning rates, prediction horizon, etc.) to explore different control behaviors.

## How to Run Code

1. Open the desired notebook (`PINN_MPC_SISO_Github_Code.ipynb` or `PINN_MPC_MIMO_Github_Code.ipynb`) in **Jupyter** or **Google Colab**.
2. Upload the corresponding training dataset files.
3. Run all cells to:
   - Train the PINN-MPC controller,
   - Evaluate it on challenging validation scenarios,
   - Visualize closed-loop behavior.
4. Modify training or simulation parameters in the relevant sections to experiment with different configurations.

**Performance Tip:** For significantly faster training, run the notebook on a **GPU**. In Google Colab, activate GPU under:
```
Runtime → Change runtime type → GPU
```

## Prerequisites
This project requires **Python 3.8+** and the following packages:
- `torch` (PyTorch ≥ 2.0)
- `numpy`
- `matplotlib`
- `scipy`

## License
This project is licensed under the **Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License**.
See the file `LICENSE-CC-BY-NC-SA.txt` for details.