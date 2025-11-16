# PINN-MPC
Code to accompany the research: **“An Explicit Model Predictive Control Framework Based on Physics-Informed Neural Networks.”**

## Table of Contents
- Overview
- Repository Structure
- Provided Notebooks
- Training & Evaluation Pipeline
- Datasets
- How to Run
- Prerequisites
- License

---

## Overview
This repository contains the full implementation of a **Physics-Informed Neural Network (PINN)** used as an explicit **Model Predictive Controller (MPC)** for nonlinear dynamical systems.

The PINN incorporates the system's differential equations directly into its loss function, enabling it to learn optimal closed-loop behavior **offline**, and act as a fast explicit MPC **online**.

The approach includes:
- Physics-based residual enforcing system dynamics
- Tracking objective toward a set-point
- Initial-condition matching
- Soft state & control constraints
- Closed-loop simulations with metrics and plots

Includes both:
- **SISO nonlinear water tank**
- **MIMO nonlinear process (research case study)**

---

## Repository Structure
```
.
├── PINN_MPC_SISO_Github_Code.ipynb      # SISO training + validation + closed-loop evaluation
├── PINN_MPC_MIMO_Github_Code.ipynb      # MIMO training + validation + closed-loop evaluation
│
├── mimo_training_samples_x.pt           # Training dataset: x0_all
├── mimo_training_samples_ysp.pt         # Training dataset: ysp_all
├── mimo_training_samples_ud.pt          # Training dataset: u0_all, d0_all, meta
│
├── mimo_test_samples.pt                 # MIMO test dataset
├── siso_training_samples.pt             # SISO training dataset
├── siso_test_samples.pt                 # SISO test dataset
│
├── LICENSE-CC-BY-NC-SA.txt
└── README.md
```

The MIMO training dataset is split across three `.pt` files so each is compatible with GitHub size limits.

---

## Provided Notebooks
### **PINN_MPC_SISO_Github_Code.ipynb**
Includes:
- Training the SISO PINN-MPC
- Physics-informed + tracking loss
- Performance metrics (RMSE, IAE, overshoot, settling time)
- Closed-loop simulation plots

### **PINN_MPC_MIMO_Github_Code.ipynb**
Includes:
- Full MIMO PINN-MPC training
- Dataset stitching (x, ysp, ud/meta)
- Evaluation on test scenarios
- Closed-loop rollouts and metrics

Both notebooks are self-contained and runnable in **Google Colab** or Jupyter.

---

## Training & Evaluation Pipeline
Each notebook implements:

### 1. Load Dataset
For MIMO:
- `mimo_training_samples_x.pt` → x0_all
- `mimo_training_samples_ysp.pt` → ysp_all
- `mimo_training_samples_ud.pt` → u0_all, d0_all, meta

### 2. Train the PINN-MPC
- Mini-batch sampling
- Autograd for physics residual
- Composite loss (physics + tracking + IC + constraints)
- Two-phase Adam training

### 3. Validation
Evaluated on:
- Set-point changes
- Disturbances
- Noise robustness

Metrics include RMSE, IAE, overshoot %, settling time.

### 4. Closed-Loop Plots
Generated after training.

---

## Datasets
### SISO
- `siso_training_samples.pt`
- `siso_test_samples.pt`

### MIMO (split into 3 files)
- `mimo_training_samples_x.pt` (x0_all)
- `mimo_training_samples_ysp.pt` (ysp_all)
- `mimo_training_samples_ud.pt` (u0_all, d0_all, meta)

### MIMO Test
- `mimo_test_samples.pt`

---

## How to Run
### **Google Colab (recommended)**
1. Upload the notebook
2. Upload required dataset files
3. Enable GPU:
```
Runtime → Change runtime type → GPU
```
4. Run all cells

### **Local Jupyter**
Install dependencies and run with Jupyter Notebook.

---

## Prerequisites
- Python 3.8+
- PyTorch 2.0+
- NumPy
- Matplotlib
- SciPy

---

## License
Licensed under **CC BY-NC-SA 4.0**. See `LICENSE-CC-BY-NC-SA.txt`.

