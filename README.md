# Geometric and Topological Analysis of MNIST

This project investigates whether image classification can be performed effectively using only geometric and topological features, ignoring raw pixel coordinates entirely.

The goal is to compare standard classification techniques against Manifold Learning and Topological Data Analysis (TDA) with respect to accuracy. We also analyze how different feature sets respond to data corruption versus elastic deformation.

## Project Overview

I compare three distinct representations of the MNIST dataset:

1.  **The Pixel View (Baseline)**
    * Treating images as flattened 784-dimensional vectors.
    * *Models:* Logistic Regression and Random Forest.
2.  **The Geometric View (Global Structure)**
    * Using **UMAP** (Uniform Manifold Approximation and Projection) to learn a lower dimensional representation of the dataset.
    * *Model:* Logistic Regression on 10 geometric features.
3.  **The Topological View (Local Structure)**
    * Using **Persistent Homology** (Cubical Persistence) to extract loops and connected components.
    * *Feature Extraction:* Betti Curves and Persistence Entropy.
    * *Model:* Random Forest on topological features.

## Key Findings

* **Signal Compression:** UMAP embeddings (10 dimensions) achieved **90.75%** accuracy with a linear model, outperforming Logistic Regression on the full 784 pixels (84.75%).
* **Topological Signal:** Topological features alone (Betti Curves) achieved **93.35%** accuracy, effectively matching the non-linear Random Forest baseline trained on raw pixels.
* **The Importance of Filtration:** Comparing Betti Curves against Persistence Entropy demonstrated that preserving the *filtration index* (geometric context) is necessary to distinguish topologically similar digits (e.g., 0 vs 6 vs 9).

## Robustness Analysis

The core of this analysis was subjecting the models to stress tests to determine feature stability.

1.  **Sensitivity to Noise:** TDA features are highly sensitive to **Salt & Pepper noise**. Random pixel corruption creates "fake" topological loops, causing accuracy to drop significantly compared to pixel-based models.
2.  **Invariance to Deformation:** TDA features are highly robust to **Elastic Deformation**. Under warping and stretching (simulating handwriting variation), topological features remained stable and outperformed the pixel baseline.

## Requirements

* Python 3.10+
* `giotto-tda`
* `umap-learn`
* `scikit-learn`
* `numpy`, `pandas`, `matplotlib`, `seaborn`, `scipy`

## Usage

To replicate the analysis:

1.  Clone the repository.
2.  Install the requirements (e.g., preferably by running the first cell in the notebook due to dependency issues or `pip install -r requirements.txt`).
3.  Run the notebook `MNIST_Geometric_Topological_Analysis.ipynb`.

The notebook will download the data, run the computations, and generate the comparison metrics and plots.

---
*Marcos Orseli*