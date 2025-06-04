---
title: "Structure from Motion (SfM)"
excerpt: "Classical computer vision based 3D reconstruction of scene from images. <br/><img src='/images/sfm/intro_merged.png' width='700'/>"
collection: projects
---

<br/><img src='/images/sfm/intro_merged.png' width='500'/>

<!-- For more details - [Project Report](https://github.com/AshwinDisa/AshwinDisa.github.io/blob/master/files/sfm_report.pdf) -->

For more details - [Project Report](https://ashwindisa.github.io/files/sfm_report.pdf)

<!-- [Github](https://github.com/Mihir-Deshmukh/SfM_NeRF/tree/main) -->

### Structure from Motion (SfM)

Implemented an end-to end pipeline for Structure from Motion to reconstruct a 3D scene from a set of images and simultaneously
obtain the camera poses of the monocular camera with respect to the given scene. Steps involved Feature Matching and Outlier
rejection using RANSAC, Estimating Fundamental using epipolar constraint and Essential Matrix, Estimate Camera Pose and
Cheirality condition using Triangulation, PnP and Bundle Adjustment. 

### Input images

Set of monocular images used for 3D reconstruction and pose estimation.
    
<br/><img src='/images/sfm_merged_4.png' width='500'/>"

### Triangulation Check for Cheirality Condition

Initial 3D points are triangulated and validated using the cheirality condition.

<br/><img src='/images/sfm/triangulation.png' width='450'/>"

### Perspective-n-Points (PnP)

Camera poses are refined using PnP with 2D-3D correspondences.

<br/><img src='/images/sfm/AfterPnP.png' width='450'/>"

### Nonlinear Reprojection

Reprojection error minimized by refining poses and 3D points nonlinearly.

<br/><img src='/images/sfm/nonlinear_reproj_1.png' width='450'/>"

### Bundle Adjustment

Global optimization of camera poses and 3D points to improve reconstruction accuracy.

<br/><img src='/images/sfm.png' width='450'/>"

Contributors: Mihir Deshmukh
