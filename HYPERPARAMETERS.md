# HYPERPARAMETERS TESTS

This document lists all the hyperparameter experiments carried out for both models:

- **MLP (Multi-Layer Perceptron)** – Target accuracy: ≥ **95%**  
- **CNN (Convolutional Neural Network)** – Target accuracy: ≥ **98%**

Each table shows the key configurations tested, their results, and short notes about stability and convergence.

# Hyperparameters

## `B` (Batch Size)
Number of images processed at once.  
→ Larger batch = more stable training, but slower.

---

## `LR` (Learning Rate)
Step size used during learning.  
→ Too large = zigzag / unstable training.  
→ Too small = very slow learning.

---

## `LR_DECAY`
When training stagnates, the learning rate is reduced.  
→ Example: `0.85` means the LR is multiplied by `0.85` (reduced by 15%).

---

## `PATIENCE`
Number of iterations to wait before reducing LR.  
→ If there’s no improvement for `PATIENCE` iterations, LR is decreased.

---

## `ANGLE`
Maximum rotation (in degrees).  
→ Helps generalization (e.g., slanted handwriting).

---

## `SCALE`
Maximum zoom variation (±).  
→ Example: `0.1` = ±10% zoom.

---

## `SHIFT`
Maximum translation (in pixels).  
→ `0.1` means 0.1 pixel (negligible).

---

## `SAMPLING`
Interpolation method for image transformations:
- `BILINEAR`: smooths pixels, slightly better for rotations.  
- `NEAREST`: keeps raw pixel values.

---

## `STEPS`
Number of training iterations (epochs).  
→ More steps = more learning, until it reaches a plateau.

---

## MLP (Multi-Layer Perceptron)

| # | Batch | LR | LR Decay | Patience | Steps | Angle | Scale | Shift (px) | Sampling | Test Accuracy (%) | Notes |
|:-:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--|
| 1 | 512 | 0.025 | 0.90 | 40 | 350 | 10 | 0.08 | 1.5 | Bilinear | **97.89** | Best balance, stable accuracy |
| 2 | 512 | 0.02 | 0.90 | 40 | 400 | 15 | 0.10 | 2.5 | Bilinear | 98.95 | High accuracy, well-regularized |
| 3 | 512 | 0.015 | 0.92 | 45 | 500 | 18 | 0.12 | 3.0 | Bilinear | 97.64 | Very stable, slightly slower training |
| 4 | 512 | 0.02 | 0.88 | 30 | 450 | 20 | 0.15 | 3.0 | Bilinear | 97.27 | Strong augmentations, robust generalization |
| 5 | 512 | 0.02 | 0.90 | 30 | 150 | 15 | 0.10 | 2.5 | Bilinear | 95.95 | Shorter training, good balance |
| 6 | 256 | 0.03 | 0.85 | 35 | 300 | 12 | 0.10 | 2.0 | Bilinear | 96.80 | Fast training, good baseline |
| 7 | 256 | 0.03 | 0.85 | 25 | 120 | 12 | 0.10 | 2.0 | Bilinear | 94.63 | Quick convergence, slightly noisy |
| 8 | 128 | 0.03 | 0.85 | 25 | 160 | 15 | 0.10 | 2.0 | Bilinear | 94.05 | Slower but low memory usage |

#1: Excellent balance, moderate LR, fast convergence, very stable.
#2: Slightly slower but well-regularized due to stronger augmentations.
#3: Very stable training, slower convergence, great for long runs.
#4: Strong augmentations improve robustness but slightly reduce fine accuracy.
#5: Fewer steps : mild underfitting, decent trade-off between speed and quality.
#6: Small batch + higher LR : fast training, a bit noisy but good accuracy.
#7: Too aggressive (high LR, low patience) : unstable convergence, lower accuracy.
#8: Very small batch : noisy gradients, slower and less stable learning.

The number of training steps is one of the most influential factors affecting the model’s final accuracy and convergence stability.

**Best configuration:** #1  
- **Accuracy:** 97.89%  
- **Loss:** 0.13
- **Batch:** 512  
- **Learning rate:** 0.025  
- **Steps:** 350  
- **Augmentation:** Mild (Angle 10°, Scale ±0.08, Shift 1.5 px)  
- **Result:** Most stable and efficient training, achieves strong accuracy with minimal overfitting.


---

## CNN (Convolutional Neural Network)

| # | Batch | LR | LR Decay | Patience | Steps | Angle | Scale | Shift (px) | Sampling | Test Accuracy (%) | Notes |
|:-:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--|
| 1 | 512 | 0.02 | 0.90 | 35 | 200 | 15 | 0.10 | 2.5 | Bilinear | 98.6 | Best trade-off: fast, stable, and accurate |
| 2 | 512 | 0.015 | 0.92 | 40 | 250 | 18 | 0.12 | 3.0 | Bilinear | **98.95** | Very stable, smooth convergence |
| 3 | 256 | 0.03 | 0.88 | 25 | 150 | 10 | 0.08 | 2.0 | Bilinear | 97.9 | Quick start, converges fast but slightly noisy |
| 4 | 512 | 0.012 | 0.92 | 40 | 280 | 15 | 0.10 | 2.5 | Bilinear | 99.0 | Low LR, excellent stability |
| 5 | 128 | 0.03 | 0.86 | 30 | 180 | 15 | 0.12 | 3.0 | Bilinear | 97.5 | Slower but consistent |


**Best configuration:** #2 (98.95%) – fast, stable, and achieves the target accuracy easily.

---

## Summary

- The **MLP** model reaches around **95–96%** accuracy without overfitting.  
- The **CNN** model consistently achieves **98–99%** test accuracy.  
- All experiments used random rotations, scaling, and shifts to improve generalization.  
- The selected final configurations (#2 for both models) were exported to **WebGPU** for deployment.
