# Neural Style Transfer Playground

This repository is a **personal playground for experimenting with neural style transfer methods**.

The current implementation is based on a classic optimization-based neural style transfer pipeline using a pretrained CNN, but the long-term goal of this project is to **compare, extend, and experiment with multiple style transfer models**.

---

## ✨ Results Preview

Below are some example results produced by the current implementation.

### Content + Style → Stylized Output

<p align="center">
  <img src="data/content/c1.jpg" width="25%">
  <img src="data/style/s2.jpg" width="27%">
  <img src="results/outputs/c1_s2.jpg" width="25%">
</p>

More examples can be found in the `data/` and `results/` directories.

---

## 🧩 What This Project Is About

Neural style transfer aims to generate an image that:

- preserves the **semantic structure** of a content image  
- adopts the **textures, colors, and brush patterns** of a style image  

Instead of training a new model, the current approach **optimizes the image itself** so that its feature representations match both content and style targets extracted from a pretrained network.

This repository is designed to evolve as I explore:
- different backbone networks
- faster feed-forward models
- more flexible arbitrary-style methods

---

## 🏗️ Current Implementation (Baseline)

At the moment, the project uses a **VGG-based neural style transfer** approach as a baseline.

### Feature Extractor
- Pretrained CNN (VGG-style architecture)
- Network weights are **frozen**
- Used only to extract intermediate feature representations

### Feature Selection
- **Content**: one deeper layer capturing spatial structure
- **Style**: multiple shallow-to-deep layers capturing textures at different scales

### Optimization Strategy
- The generated image is initialized from the content image
- Losses are computed and backpropagated **only to the image**
- Optimized using **L-BFGS**

---

## 📉 Loss Behavior & Runtime Observation

During experimentation, I observed that:

- Most loss terms converge **much earlier than expected**
- After ~300 iterations, visual changes become minimal
- Increasing iterations mainly increases runtime without clear benefits

Based on this, the default number of optimization steps was reduced, significantly improving efficiency while maintaining visual quality.

<p align="center">
  <img src="results/Loss_Curves.jpg" width="70%">
</p>

---

## 🧪 Experiments on Custom Images

The model was tested on both provided examples and personal images, including:

- Architectural scenes
- Indoor photos
- Images with strong vs. minimal texture styles

**Key observation:**
> Style images with rich, high-frequency textures transfer much more strongly than simple or flat styles.


