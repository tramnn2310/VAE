# Automated Defect Detection in Nanomaterial-Coated Fabrics Using Variational Autoencoder

## Overview

This repository contains the implementation of an **unsupervised defect detection framework** for **nanomaterial-coated fabrics**, developed as part of my **Master’s thesis** and subsequent academic paper:

> *Automated Defect Detection in Nanomaterial-Coated-Fabrics Using Variational Autoencoder*

The proposed method applies a **Variational Autoencoder (VAE)** combined with **image post-processing techniques** to automatically detect regions with **abnormally high nanomaterial density** on coated cotton fabrics, which can negatively impact the performance and safety of smart textile applications.

---

## Problem Motivation

Smart textiles coated with nanomaterials such as **single-walled carbon nanotubes (SW-CNT)** are widely used in:

- Wearable health monitoring
- Textile electrodes for bio-signal acquisition
- Responsive and sensing garments

However, **manual coating processes** often introduce **local regions with excessive particle density**, leading to:
- Electrical instability
- Signal distortion
- Safety risks in wearable applications

Detecting these defective regions is challenging because:
- Defect labels are unavailable or application-dependent
- Defects exhibit irregular shapes and sizes
- Traditional rule-based image processing lacks robustness

This work addresses these challenges using an **unsupervised deep learning approach**.

---

## Why Variational Autoencoder (VAE)

A **Variational Autoencoder** was selected due to its ability to:

- Learn the **dominant distribution of fabric textures** without labels
- Encode images into a **regularized latent space**
- Reconstruct defect-free representations of coated fabrics

Key assumption:
- The VAE learns dominant (non-defective) features
- Regions with abnormal particle density produce **reconstruction discrepancies**
- These discrepancies can be exploited to localize defects

---

## Methodology

### 1. Data Acquisition & Preprocessing

- Cotton fabrics coated with commercial **SW-CNT**
- Fabric samples scanned using a flatbed scanner
- Images converted to grayscale and enhanced using **contrast stretching**
- Images divided into fixed-size patches for training

---

### 2. VAE Architecture

The VAE consists of:

- **Encoder**  
  - 2D convolutional layers with ReLU and batch normalization  
  - Outputs latent mean and variance

- **Latent Space**  
  - Gaussian prior  
  - Reparameterization trick for stochastic sampling

- **Decoder**  
  - Transposed convolution layers  
  - Reconstructs dominant fabric features

The loss function combines:
- Reconstruction loss
- KL-divergence regularization

---

### 3. Training Strategy

- Trained on **unlabeled scanned fabric images**
- Dataset includes both normal and defective regions, but:
  - Dominant (non-defective) patterns are learned
- No explicit defect annotations are required

---

### 4. Defect Localization (Post-Processing)

After reconstruction:

1. The original image and reconstructed image are **summed**
2. Bright regions correspond to normal fabric
3. Dark regions correspond to potential defects
4. Defective regions are extracted using:
   - Intensity thresholding in HSV color space
   - Morphological filtering
   - Connectivity analysis

This hybrid approach improves localization accuracy compared to raw reconstruction error alone.

---

## Experimental Validation

### Ground Truth Definition

- Defective regions were defined based on:
  - **Sheet resistance measurements**
  - **Electrical safety and signal quality experiments**
- Regions with resistance deviation exceeding **45%** were labeled as defective

---

## Results

The proposed method achieved:

- **Recognition rate:** **93.2%**
- **Intersection over Union (IoU):**
  - Up to **0.923** for high-density defect regions
  - Average IoU of **0.76** across the test dataset

Key observations:
- Accurate localization of high-density nanomaterial regions
- Robust performance despite limited training data
- Effective separation of defective vs non-defective areas

These results validate the effectiveness of combining **VAE-based feature learning** with **image post-processing** for defect detection in coated fabrics.

---

## Key Contributions

- Proposed an **unsupervised defect detection framework** for nanomaterial-coated fabrics
- Demonstrated VAE effectiveness without defect-free training data
- Introduced a practical post-processing pipeline for defect localization
- Validated results through **electrical and morphological experiments**
- Advanced quality control techniques for smart textile applications

---

## Technologies Used

- Python / MATLAB (R2021b)
- Variational Autoencoder (CNN-based)
- NumPy
- Image processing techniques (thresholding, morphology)
- Jupyter Notebook

---

## How to Run

1. Clone the repository
2. Open the notebook:

   ```bash
   VAE.ipynb
