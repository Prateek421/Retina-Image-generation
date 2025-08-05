# Comparative Study of Retinal Image Generation using DCGAN and Diffusion Models

## Overview
This repository contains two research implementations exploring generative models for synthetic retinal image generation:
1. **Retina Diffusion Model Implementation** – based on Denoising Diffusion Probabilistic Models (DDPMs).
2. **Retinal Image Generation using DCGAN** – based on Deep Convolutional Generative Adversarial Networks (DCGANs).

The primary aim is **methodological comparison** rather than providing deployable code. The work investigates each model’s ability to generate realistic retinal fundus images for **research and academic analysis**.

---

## Research Motivation
Retinal imaging is vital in diagnosing conditions such as diabetic retinopathy, glaucoma, and age-related macular degeneration.  
However, **scarcity of large, annotated datasets**—due to privacy concerns and resource-intensive labeling—limits the development of robust deep learning solutions.  
Synthetic data generation offers a potential remedy by:
- Augmenting existing datasets.
- Preserving patient privacy.
- Enabling controlled experimental environments.

---

## Dataset
- **STARE (Structured Analysis of the Retina)** – 397 high-resolution retinal fundus images.
- Augmentation: rotations (±15°), horizontal/vertical flips.
- Final dataset size after augmentation: **1191 images** (resized to 256×256 pixels).

---

## Methodology

### 1. Diffusion Model (DDPM)
- Implemented using HuggingFace **diffusers** library.
- U-Net architecture with attention mechanisms.
- Training:
  - Epochs: 100
  - Timesteps: 1000
  - Optimizer: AdamW
  - Loss: Mean Squared Error (MSE)
- Focus: High structural accuracy and perceptual quality.

### 2. DCGAN
- Generator: Transposed convolutions, BatchNorm, ReLU, Tanh output.
- Discriminator: Convolutional layers, BatchNorm, LeakyReLU.
- Training:
  - Epochs: 100
  - Optimizer: Adam
  - Loss: BCEWithLogitsLoss
- Focus: Faster generation and higher diversity.

---

## Evaluation Metrics
Models were compared using:
- **FID** (Fréchet Inception Distance) – lower is better.
- **KID** (Kernel Inception Distance) – lower is better.
- **SSIM** (Structural Similarity Index) – higher is better.
- **Diversity Score** – higher indicates more varied outputs.

| Model       | Best FID | Best SSIM | Best Diversity |
|-------------|----------|-----------|----------------|
| **DDPM**    | 400.88   | 0.3593    | 0.2087         |
| **DCGAN**   | 956.63   | 0.2785    | 0.3577         |

---

## Key Findings
- **DDPM** produced images with better structural similarity (SSIM) and more realistic distributional alignment (FID).
- **DCGAN** generated more diverse images but with less structural accuracy.
- High FID values for both models partly due to the small validation set size, leading to score variance.

---