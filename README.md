# AI600: Deep Learning Assignment 2

**Student Name:** Syed Obaidullah Hassan Chishti
**Student ID:** 25280049

## Overview
This repository contains Assignment 2 for the AI600: Deep Learning course. The assignment is implemented in a Jupyter notebook (`main.ipynb`).

## What’s in here

- **`main.ipynb`**: end-to-end workflow (data loading → feature extraction → model training → evaluation → test inference).
- **`requirements.txt`**: Python dependencies used for the run.

## Dataset / expected files

The notebook expects the following files (not committed; ignored via `.gitignore`):

```
processed_data/
  quickdraw_train.npz
  quickdraw_test.npz
```

Expected keys used by the notebook:

- **`quickdraw_train.npz`**: `x_train`, `y_train`, `class_names`

## Setup

The notebook run with **Python 3.13.3**.

Create and activate a virtual environment, then install dependencies:

```bash
python -m venv .venv
# Windows PowerShell
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### PyTorch note (CUDA wheels)

`requirements.txt` pins `torch==2.7.1+cu118` and `torchvision==0.22.1+cu118`. If `pip install -r requirements.txt` fails because it can’t find the `+cu118` build, install PyTorch using the official CUDA index first, then install the remaining packages:

```bash
pip install torch torchvision --index-url "https://download.pytorch.org/whl/cu118"
pip install -r requirements.txt
```

If you don’t have CUDA, install a CPU build instead.

## How to run

Open and run the notebook:

```bash
jupyter notebook main.ipynb
```

Recommended order inside `main.ipynb`:

- **Data loading**: loads the `.npz` files from `processed_data/`
- **Training**: trains `ChampionModel` and logs artifacts for the run
- **Evaluation**: computes test accuracy, classification report, and confusion matrix
- **Inference**: loads a saved `final_model.pt` and writes `predictions.txt`

## Outputs / artifacts

During training, a timestamped run folder is created:

```
logs/YYYYMMDD_HHMMSS/
  config.json
  metrics.json
  model_structure.json
  model_summary.txt
  confusion_matrix.png
  test_results.txt
  models/
    model_epoch_<N>.pt
    final_model.pt
  plots/
    loss_curve.png
    accuracy_curve.png
```

Inference writes:

- **`predictions.txt`**: comma-separated predicted class indices for the test set.

## Reproducibility notes

- **Notebook hardcoded paths**: the inference section uses a hardcoded `MODEL_PATH` like `logs/<timestamp>/models/final_model.pt`. Update this path to point to the run you want to use.
- **Git ignores**: `processed_data/` and most of `logs/` are intentionally ignored (see `.gitignore`).