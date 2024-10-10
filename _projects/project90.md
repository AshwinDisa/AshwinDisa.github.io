---
title: "Road scene understanding from a monocular camera"
excerpt: "Leveraging deep learning techniques for ADAS <br/><img src='/images/einstein_vision.png' width='400'/>"
collection: projects
---

🏆 Received best project award.

[Report link](https://pear.wpi.edu/img/teaching/rbe549/spring2024/studentoutputs/p3ph3/group6.pdf)

The project is inspired by Tesla’s dashboard focusing on enhancing essential autonomous driving features contributing to the development of safer and more efficient ADAS technologies.

Leveraging deep learning techniques for autonomous driving, including YOLO, DETIC for object detection (cars, road signs, traffic signals), Marigold for monocular depth estimation, OSX for pedestrian pose estimation and mask RCNN for lane detection and classification and RAFT for optical flow to create a 3D representation of the driving scene. Integrated this data into Blender for visualization.

## Overall pipeline

<img src='/images/einstein_vision/einstein_vision_pipeline.png' width='600'/>

## Monocular depth: Marigold

[Link](https://github.com/prs-eth/Marigold)

We utilized this model to get scaled depth following the instrutions on the github repo. We save these depth maps to project pixel coordinates to real world for the various detections.

<img src='/images/einstein_vision/marigold.png' width='400'/>

## Object Detection -> Instance Segmentation: DETIC

[Link](https://github.com/facebookresearch/Detic)

We utilized DETIC to do instance segmentation. We get car subtypes like SUV, sedan, hatchback, pickup_truck using custom vocabulary. We also get stop sign, motorcycle, bicycle, traffic cones, cylinder etc from this model. The centroid of these masks is then projected to 3D space using the depth from the previous model.

<img src='/images/einstein_vision/detic.png' width='400'/>

## Lane Detection: Mask RCNN

[Link](https://debuggercafe.com/lane-detection-using-mask-rcnn/)

We used this MASK RCNN trained on custom lane detection dataset from the given link for lane detection. This returns the type of lane i.e solid, dotted, divider line and double line which we use to plot them accordingly. We also get road-signs i.e signs on the road surface.

<img src='/images/einstein_vision/lane.png' width='400'/>

## 3D bounding box: For vehicle orientation

[Link](https://github.com/skhadem/3D-BoundingBox)

We use this implementation of YOLO3d to get the orientation of the vehicles. We pass the bounding boxes from DETIC to the regressor which predicts 3D bounding box. We use the yaw from this to spawn the cars with orientations.

<img src='/images/einstein_vision/bounding_box.png' width='400'/>

## Traffic Light detection: YOLOV3

[Link](https://github.com/sovit-123/Traffic-Light-Detection-Using-YOLOv3)

We use this mdoel trained on LISA traffic light dataset fro traffic light detection. It detects go, goLeft, stop, stopLeft warning and warningLeft which we use to spawn the corresponding traffic light colors and arrows.

<img src='/images/einstein_vision/traffic_light.png' width='400'/>

## Road Signs detection: YOLOV8

[Link](https://universe.roboflow.com/dakota-smith/lisa-road-signs)

We use the pretrained YoloV8 weights from the GLARE dataset paper for identifying various traffic signs like speed limit, pedestrain crossing etc. For speed bump detection we used a custom version of LISA dataset we found on ROBOFLOW and trained a YOLOv8 on that. It has a specific class for identifying speed bump signs. We aggregated the speed bump detections from this with the GLARE model.

<img src='/images/einstein_vision/road_sign.png' width='400'/>

## Human pose estimation: OSX

 We use the OSX implemenatation which generates the blend file for the humans in the image. This captures intricate movements in a better manner.

[OSX Link](https://github.com/IDEA-Research/OSX)

 <img src='/images/einstein_vision/osx.png' width='400'/>

[YOLO NAS POSE Link](https://github.com/Deci-AI/super-gradients/blob/master/YOLONAS-POSE.md)

<img src='/images/einstein_vision/yolonaspose.png' width='400'/>

## RAFT: Optical Flow

 [Link](https://github.com/princeton-vl/RAFT)

 We use this to calculate optical flow which is used to identify if the car is moving or not. We use a classical apporach for tail light detection.

 <img src='/images/einstein_vision/raft.png' width='400'/>

Parked and moving vehicles detections from optical flow.

 <img src='/images/einstein_vision/optical_flow.png' width='400'/>

Contributors: Mihir Deshmukh
