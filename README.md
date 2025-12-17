# Fabric Defect Detection Using Variational Autoencoder (VAE)

## Overview

This repository contains an implementation of a **Variational Autoencoder (VAE)** for **unsupervised anomaly detection** on fabric images.  
The project was developed as part of my **Master’s thesis**, with the goal of detecting surface defects in textile materials without relying on labeled defect data.

The approach trains a generative model on **normal (defect-free) fabric images only**, then identifies anomalies based on reconstruction quality.

---

## Problem Statement

In industrial textile inspection:

- Defective samples are rare, diverse, and expensive to label
- Supervised learning approaches require large, balanced datasets
- Traditional rule-based image processing struggles with complex textures

This project addresses these challenges by applying **unsupervised learning**, enabling defect detection without explicit defect annotations.

---

## Why Variational Autoencoder (VAE)

A Variational Autoencoder was selected because:

- It learns a **probabilistic latent representation** of normal fabric textures
- Latent space regularization improves generalization to unseen data
- Reconstruction-based anomaly detection is effective for subtle texture defects

**Key assumption**:  
- Normal fabric patterns are well reconstructed  
- Defective patterns produce higher reconstruction error

---

## Methodology

### 1. Data Preparation

- Input data consists of fabric images
- Images are resized and normalized
- Only **non-defective (normal)** samples are used during training

---

### 2. Model Architecture

The VAE consists of:

- **Encoder**: maps input images to a latent distribution (mean and variance)
- **Latent space**: sampled using the reparameterization trick
- **Decoder**: reconstructs images from latent vectors

The loss function combines:

- **Reconstruction loss** (pixel-level difference)
- **KL divergence loss** (latent space regularization)

---

### 3. Training Process

- The model is trained exclusively on normal fabric images
- The VAE learns the distribution of defect-free textures
- No defect labels are required during training

---

### 4. Anomaly Detection

During inference:

1. Images are passed through the trained VAE
2. Reconstruction error is calculated for each image
3. Images with high reconstruction error are flagged as anomalies

---

## Results

The trained model demonstrates:

- Accurate reconstruction of normal fabric textures
- Degraded reconstruction in defective regions
- Clear separation between normal and anomalous samples using reconstruction error

Qualitative analysis shows that defects such as:

- Local texture irregularities
- Structural distortions
- Abnormal surface patterns

are effectively detected through reconstruction differences.

This validates the suitability of VAE-based models for **unsupervised textile defect detection**.

---

## Key Contributions

- Implemented an end-to-end VAE pipeline for fabric anomaly detection
- Demonstrated unsupervised learning without defect labels
- Validated reconstruction-based anomaly scoring
- Proposed a scalable solution for industrial inspection systems

---

## Technologies Used

- Python  
- Deep Learning Framework (TensorFlow)
- Keras, NumPy  
- OpenCV  
- Jupyter Notebook  

---

## How to Run

1. Clone this repository
2. Install required dependencies
3. Open the notebook:

   ```bash
   VAE.ipynb
