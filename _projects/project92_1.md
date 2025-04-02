---
title: "Panorama stitching"
excerpt: "Stitch two or more images to create seamless panorama image.<br/><img src='/images/panorama/merged_all.png' width='700'/>"
collection: projects
---

For more details - [Project Report](https://ashwindisa.github.io/files/panorama_report.pdf)

[Github](https://github.com/AshwinDisa/RBE549_AutoPano)

### Input data

Monocular images with 30 − 50% overlap.

<br/><img src='/images/panorama/dataset.png' width='600'/>"

### Corner detection

Harris corner & Adaptive Non-maximal Suppression (ANMS) for uniform distribution of features

<br/><img src='/images/panorama/corners.png' width='450'/>"

### Feature matching and RANSAC for outlier rejection

Match keypoints (encoded as feature vectors) across pair of images. Refine the matches using RANSAC. 

<br/><img src='/images/panorama/matching_merged.png' width='650'/>"

### Stitch all images

Estimated homography using the refined matches, warp and stitch images with overlap.

<br/><img src='/images/panorama/pano1.png' width='500'/>"

### More panoramas

<br/><img src='/images/panorama/more_pano_merged.png' width='600'/>"

