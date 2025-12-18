# Unsupervised Defect Detection on Nanomaterial-Coated Fabrics (VAE)

## TL;DR

- Built an **end-to-end unsupervised anomaly detection pipeline** using a Variational Autoencoder (VAE)
- Applied to **real industrial fabric images** with no defect labels
- Combined **deep learning + classical image processing** for robust localization
- Achieved **93.2% defect recognition rate** and **IoU up to 0.923**
- Project originated from a **Master’s thesis + published research**, implemented as a reproducible Jupyter Notebook

---

## Project Overview

This repository implements an **unsupervised defect detection system** for **nanomaterial-coated fabrics**, designed for use cases where:

- Defect labels are unavailable or application-dependent
- Defects have **irregular shapes and sizes**
- Visual appearance correlates with **functional degradation** (e.g., electrical instability)

The system uses a **Variational Autoencoder (VAE)** to learn dominant fabric textures and detects anomalies through **reconstruction discrepancies**, followed by targeted post-processing to extract defect regions.

This project demonstrates **full pipeline ownership**, from data preprocessing to model training, inference, and evaluation.

---

## Business / Engineering Motivation

In smart textile and manufacturing contexts:

- Manual coating processes introduce **localized defects**
- These defects impact **signal quality, safety, and reliability**
- Supervised inspection systems are costly and brittle due to labeling requirements

This project addresses those constraints by using:
- **Unsupervised learning**
- **Minimal assumptions about defect shape**
- **Hybrid ML + image processing techniques**

The approach generalizes to other surface-inspection problems beyond textiles.

---

## System Design

### 1. Data Handling & Preprocessing

- Input: scanned images of coated cotton fabric
- Convert RGB → grayscale
- Apply **contrast stretching** to amplify defect-related intensity differences
- Split full images into fixed-size patches for training stability

---

### 2. Model Architecture (VAE)

- **Encoder**
  - CNN-based feature extractor
  - Outputs latent mean and variance
- **Latent Space**
  - Gaussian prior
  - Reparameterization trick for backpropagation
- **Decoder**
  - Transposed convolutions
  - Reconstructs dominant (non-defective) fabric patterns

Loss function:
- Reconstruction loss
- KL-divergence regularization

The model is trained **without defect labels**.

---

### 3. Inference & Defect Localization

Rather than relying on raw reconstruction error alone, the pipeline:

1. Reconstructs the input image using the trained VAE
2. Combines original and reconstructed images to enhance contrast
3. Applies:
   - Intensity thresholding (HSV space)
   - Morphological filtering
   - Connectivity constraints
4. Outputs a **binary defect mask** aligned with functional defect regions

This hybrid approach improves localization robustness in noisy, real-world data.

---

## Notebook: `EN_VAE_Anomalydetection.ipynb`

- Full implementation of the pipeline
- Converted from the original **MATLAB Live Script**
- Organized as a **research-grade, step-by-step workflow**:
  - Image preprocessing
  - Patch extraction
  - VAE definition and training
  - Reconstruction
  - Post-processing and visualization

The notebook prioritizes **clarity and reproducibility** over production optimization.

---

## Results

- **Defect recognition rate:** **93.2%**
- **Intersection over Union (IoU):**
  - Up to **0.923** for high-density defect regions
  - Average IoU **0.76** across test data

Ground truth was defined using **electrical measurements and functional validation**, not manual pixel labeling.

These results demonstrate that the model learns **functionally meaningful anomalies**, not just visual noise.

---

## Technologies & Tools

- Python
- Variational Autoencoder (CNN-based)
- Image processing (thresholding, morphology)
- Jupyter Notebook
- MATLAB (original experimental implementation)

---

