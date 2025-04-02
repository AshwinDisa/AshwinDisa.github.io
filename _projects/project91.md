---
title: "Neural Radiance Field (NeRFs)"
# excerpt: "Deep learning based 3D reconstruction and novel view synthesis.<br/><img src='/images/nerf/nerf.png' width='300'/>"
excerpt: "Deep learning based 3D reconstruction and novel view synthesis.<br/><br/><img src='/images/nerf/colmap.png' width='350'/><img src='/images/nerf/lego_indefinite.gif' width='350' />"

collection: projects
---

<!-- For more details - [Project Report](https://github.com/AshwinDisa/AshwinDisa.github.io/blob/master/files/sfm_report.pdf) -->

For more details - [Project Report](https://ashwindisa.github.io/files/sfm_report.pdf)

<!-- [Github](https://github.com/Mihir-Deshmukh/SfM_NeRF/tree/main) -->


Implemented the modern deep learning approach using Neural Radiance Fields (NeRF) for photo realistic visualization
and synthesize novel views of complex scenes.

### Neural Radiance Field (NeRF)

Each image pixel is converted into rays using camera parameters and a MultiLayer Perceptron (MLP) neural network is trained to predict color and density values along each ray. Using volume rendering, these values are accumulated to reconstruct images from unseen viewpoints. 

The model, based on the original NeRF architecture with positional encoding and skip connections, achieved high fidelity on the Lego and Ship datasets with PSNR scores of 25.51 and 26.95, respectively.

<br/><img src='/images/nerf1.png' width='600'/>"

<div style="display: flex; gap: 20px;">
  <img src="/images/nerf/lego_indefinite.gif" width="300" />
  <img src="/images/nerf/ship_indefinite.gif" width="300" />
</div>

### 3D reconstruction using COLMAP 

<br/><img src='/images/colmap.png' width='600'/>"

Contributors: Mihir Deshmukh
