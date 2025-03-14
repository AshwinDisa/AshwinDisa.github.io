---
title: "Structure from Motion (SfM) and NeRF"
excerpt: "3D reconstruction of scenes from images and novel view synthesis.<br/><img src='/images/colmap_nerf_merge.png' width='700'/>"
collection: projects
---

[Project Report](https://pear.wpi.edu/img/teaching/rbe549/spring2024/studentoutputs/p2ph2/group6.pdf)

[Github](https://github.com/Mihir-Deshmukh/SfM_NeRF/tree/main)

### Structure from Motion (SfM)

Implemented an end-to end pipeline for Structure from Motion to reconstruct a 3D scene from a set of images and simultaneously
obtain the camera poses of the monocular camera with respect to the given scene. Steps involved Feature Matching and Outlier
rejection using RANSAC, Estimating Fundamental using epipolar constraint and Essential Matrix, Estimate Camera Pose and
Cheirality condition using Triangulation, PnP and Bundle Adjustment. 

#### Input images

<br/><img src='/images/sfm_merged_4.png' width='600'/>"

#### Reconstructed scene

<br/><img src='/images/sfm.png' width='600'/>"

### Neural Radiance Field (NeRF)

Implemented the modern deep learning approach using Neural Radiance Fields (NeRF) for photo realistic visualization
and synthesize novel views of complex scenes.

<br/><img src='/images/nerf1.png' width='600'/>"

### NeRF using COLMAP

Reconstructed the same scene using COLMAP.

<br/><img src='/images/colmap.png' width='600'/>"

Contributors: Mihir Deshmukh
