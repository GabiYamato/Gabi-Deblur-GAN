# Gabi-Deblur-GAN

## Overview

**Gabi-Deblur-GAN** is a deep learning project for image deblurring using a highly configurable Generative Adversarial Network (GAN) implemented in PyTorch. The model is designed to restore sharp images from blurred inputs, leveraging advanced architectural features and training strategies to achieve state-of-the-art results.

---

## Features

- **GAN Architecture**: Consists of a U-Net-based Generator and a PatchGAN Discriminator.
- **Parameter-rich Design**: Combined generator and discriminator have over 100 million parameters for high capacity.
- **Configurable**: All hyperparameters and architectural choices are set in a single Python dictionary (`CONFIG`), making experimentation easy.
- **Advanced Blocks**: Includes Residual, Dense, and Attention blocks for improved learning and feature representation.
- **Loss Functions**: Uses adversarial loss, L1 loss, and perceptual loss (VGG19-based) for balanced training.
- **Training Enhancements**:
  - Early stopping to prevent overfitting.
  - Learning rate schedulers for adaptive training.
  - Periodic saving of sample outputs and model checkpoints.
- **Progress Visualization**: Automatically saves deblurred image samples every 5 epochs for visual monitoring.
- **Direct Model Access**: No class wrappers—models, optimizers, and functions are accessible directly for simplicity.

---

## Dataset

- **GoPro Dataset**: The project uses the GoPro dataset, containing paired blurred and sharp images.
- **Custom PyTorch Dataset**: Handles both `blur` and `blur_gamma` directories, pairing each blurred image with its corresponding sharp ground truth.
- **Transformations**: Images are resized to 256×256, converted to tensors, and normalized to [-1, 1].

---

## Model Architecture

### Generator

- **U-Net Backbone**: Deep encoder-decoder structure with skip connections.
- **Dense Blocks**: Added for increased parameter count and feature reuse.
- **Residual Blocks**: Improve gradient flow and stability.
- **Attention Blocks**: Capture global context and enhance feature learning.
- **Output**: Produces a sharp RGB image from a blurred input.

### Discriminator

- **PatchGAN**: Operates on local image patches for fine texture discrimination.
- **Spectral Normalization**: Stabilizes GAN training.
- **Extra Convolutions**: Deep, wide layers for increased capacity.

### Losses

- **Adversarial Loss**: Standard GAN loss for realism.
- **L1 Loss**: Pixel-wise difference for fidelity.
- **Perceptual Loss**: Feature-level similarity using VGG19.

---

## Training

- **Direct Functions**: Training, validation, and visualization are handled by standalone functions.
- **Early Stopping**: Stops training if validation loss does not improve for a set number of epochs.
- **Learning Rate Scheduling**: Reduces learning rate on plateau.
- **Sample Output Saving**: Every 5 epochs, saves a grid of blurred, generated, and ground truth images for 10–20 random validation samples.
- **Checkpoints**: Best model and periodic checkpoints are saved automatically.

---

## Usage

### 1. Setup

- Install dependencies:
  ```
  pip install torch torchvision matplotlib numpy opencv-python
  ```
- Place the GoPro dataset in the `Dataset/train` and `Dataset/test` folders as described.

### 2. Configuration

- All hyperparameters and architectural choices are set in the `CONFIG` dictionary in `model_training.ipynb`.
- Change values as needed for experimentation (e.g., depth, channels, learning rates).

### 3. Training

- Run `model_training.ipynb` in VS Code or Jupyter.
- The notebook will:
  - Load and preprocess the dataset.
  - Initialize models and optimizers.
  - Start training and periodically save outputs and checkpoints.

### 4. Monitoring

- **Sample Outputs**: Check the `sample_outputs` folder for progress images every 5 epochs.
- **Training History**: Loss curves and learning rates are plotted and saved as `training_history.png`.
- **Checkpoints**: Best and periodic models are saved in the `checkpoints` folder.

---

## Customization

- **Model Architecture**: Modify the generator/discriminator classes for different blocks or depths.
- **Loss Functions**: Add or remove losses as needed.
- **Training Loop**: Adjust batch size, number of epochs, or add new callbacks.

---

## Tips

- For best results, use a CUDA-enabled GPU.
- Adjust `batch_size` and `gen_base_channels` according to your GPU memory.
- Use the saved sample images to visually inspect model progress and avoid overfitting.

---

## File Structure

```
Gabi-Deblur-GAN/
│
├── Dataset/
│   ├── train/
│   └── test/
├── sample_outputs/
├── checkpoints/
├── model_training.ipynb
├── README.MD
└── ...
```

---

## Credits

- **GoPro Dataset**: [https://seungjunnah.github.io/Datasets/gopro.html](https://seungjunnah.github.io/Datasets/gopro.html)
- **PyTorch**: [https://pytorch.org/](https://pytorch.org/)
- **VGG19**: Used for perceptual loss.

---

## License

This project is for research and educational purposes. Please cite the original GoPro dataset and any referenced architectures
