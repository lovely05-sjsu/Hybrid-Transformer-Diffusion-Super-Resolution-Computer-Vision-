# Hybrid-Transformer-Diffusion-Super-Resolution

Deep Learning Project — Hybrid Transformer–Diffusion Architecture for Efficient Super-Resolution

## Overview

Single Image Super-Resolution (SISR) focuses on reconstructing a **high-resolution (HR) image from a low-resolution (LR) input** while preserving structural details and realistic textures.

Traditional super-resolution models such as CNNs and Transformer-based approaches achieve strong reconstruction metrics but often produce **overly smooth textures**. Diffusion-based models generate realistic textures but require **slow multi-step denoising**, making them impractical for real-time applications.

This project proposes a **Hybrid Transformer–Diffusion Super-Resolution Model** that combines:

- **SwinIR Transformer Network** for structural reconstruction
- **SR3 Diffusion Model** for texture refinement

The hybrid approach bridges the **quality–speed trade-off**, producing sharper textures while maintaining near real-time performance.

---

## Project Goals

- Convert **Low Resolution (LR)** images into **High Resolution (HR)** images.
- Preserve structural fidelity while enhancing fine textures.
- Combine deterministic super-resolution with diffusion-based refinement.
- Achieve high-quality results with efficient runtime.

---

## Applications

- Medical imaging enhancement (MRI, CT scans)
- Satellite and remote sensing imagery
- Surveillance and security video enhancement
- Photography and image restoration
- Edge AI vision systems

---

## Model Architecture

The proposed pipeline consists of two stages:

### Stage 1 — Transformer Super-Resolution
A SwinIR transformer network generates an initial high-resolution reconstruction from the LR image.

### Stage 2 — Diffusion-Based Refinement
A modified SR3 diffusion network performs lightweight deterministic refinement to enhance textures.

---

## Dataset

Training and evaluation use commonly adopted super-resolution datasets.

### Training Dataset

DF2K dataset:
- DIV2K (800 images)
- Flickr2K (2650 images)

Total training images: **3450**

Low-resolution images are generated using **bicubic downsampling with ×4 scaling**.

### Evaluation Datasets

- DIV2K Validation
- Set14
- BSD100
- Urban100

These datasets provide diverse scenes and textures for benchmarking super-resolution models.

---

## Evaluation Metrics

### Image Quality Metrics

| Metric | Description |
|------|------|
| PSNR | Measures pixel-level reconstruction accuracy |
| SSIM | Evaluates structural similarity |
| LPIPS | Measures perceptual similarity |

### Efficiency Metrics

| Metric | Description |
|------|------|
| Runtime (ms) | Average inference time per image |
| Parameters | Model size |

---

## Model Comparison

| Model | Parameters | Strength | Limitation |
|------|------|------|------|
| SwinIR | 0.79M | Fast, strong structural accuracy | Smooth textures |
| SR3 | 4.5M | Rich perceptual textures | Slow inference |
| Hybrid Model | 5.32M | Balanced quality and efficiency | Slightly slower than SwinIR |

---

## Experimental Results

### Image Quality

| Dataset | SwinIR PSNR | Hybrid PSNR |
|------|------|------|
| DIV2K Validation | 27.52 | **27.65** |
| Set14 | 25.05 | **25.21** |
| BSD100 | 25.34 | **25.41** |
| Urban100 | 22.51 | **22.64** |

The hybrid model improves **PSNR and SSIM across benchmark datasets**.

---

### Runtime Comparison

| Dataset | SwinIR | SR3 | Hybrid |
|------|------|------|------|
| DIV2K Validation | 6.47 ms | 4417 ms | 20.45 ms |
| Set14 | 5.34 ms | 350 ms | 19.85 ms |

## Key observations:

- Hybrid model is **3–4× slower than SwinIR**
- Hybrid is **~200× faster than SR3 diffusion**
- Provides strong **quality vs efficiency trade-off**

---

## Installation

Clone the repository

Install dependencies:
pip install -r requirements.txt


Main dependencies:

- Python 3.9+
- PyTorch
- torchvision
- numpy
- matplotlib
- lpips
- opencv-python

---

## Running the Project

### 1. Dataset Preparation

Run the dataset setup notebook:
DL_DATA_setup.ipynb

This notebook generates low-resolution images from HR images using bicubic downsampling.

### 2. Model Training

Run the training notebook:

Model_training.ipynb

The notebook includes:

- SwinIR training
- SR3 diffusion training
- Hybrid model inference and evaluation

---

## Limitations

- Current NPU toolchains do not fully support transformer and diffusion operations.
- Deployment on Mobilint Aries NPU was unsuccessful due to unsupported operators.
- The model currently runs efficiently only on GPU environments.

---

## Future Work

- Adaptive refinement based on texture complexity
- Joint training of SwinIR and diffusion refiner
- Testing under real-world degradations (noise, blur, compression)
- Hardware-aware model optimization for edge deployment


---

## References

Key research papers referenced in this project:

- SwinIR: Image Restoration Using Swin Transformer
- SR3: Image Super-Resolution via Iterative Refinement
- EDSR: Enhanced Deep Residual Networks for Super-Resolution



