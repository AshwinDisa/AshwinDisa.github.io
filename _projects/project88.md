---
title: "Optimized inference using ONNX Runtime and TensorRT"
excerpt: "Crucial for time critical applications like Autonomous Driving.<br> <br/><img src='/images/tensorrt/P3scene7.gif' width='700'/>"
collection: projects0
---

<img src='/images/tensorrt/P3scene7.gif' width='800'/>

## Introduction

This project is focused on converted a ResNet18-based [CLRNet](https://github.com/Turoad/CLRNet) pre-trained model in PyTorch, (weights can be found [here](https://github.com/turoad/CLRNet/releases)) trained on the [CULane](https://xingangpan.github.io/projects/CULane.html) dataset for lane detection to ONNX and TensorRT engine with 16-bit floating-point (FP16) quantization for optimized inference.


- Original paper - [pdf](https://arxiv.org/pdf/2203.10350)

- To recreate - [Github](https://github.com/AshwinDisa/CLRNet/tree/main), follow - [readme](https://github.com/AshwinDisa/CLRNet/blob/main/myREADME.md) 

### ONNX Runtime

A high-performance inference engine designed to run machine learning models represented in the Open Neural Network Exchange (ONNX) format. It supports cross-platform execution across CPUs and GPUs, and is optimized for speed and portability. In this project, ONNX Runtime is used to run the converted lane detection model on both CPU and GPU, providing an easy and flexible way to evaluate performance without requiring significant changes to the codebase. It enables direct inference on NumPy arrays and abstracts GPU management, making it ideal for rapid prototyping and deployment testing.

### TensorRT

NVIDIA’s deep learning inference SDK specifically optimized for GPU acceleration. It supports FP16 and INT8 quantization, kernel fusion, and layer optimizations to maximize throughput and reduce latency on NVIDIA hardware. In this project, the lane detection model is further optimized and deployed using TensorRT, achieving real-time inference at 141 FPS on an RTX 4060 GPU. By converting the ONNX model into a TensorRT engine and using lower-precision computation, TensorRT significantly reduces inference time, making it highly suitable for high-performance and real-time applications like autonomous driving. 

## Results
### Inference Performance

| Inference Backend | Device         | Mean FPS     | Inference Time (approx.) |
|-------------------|----------------|---------|---------------------------|
| TensorRT          | RTX 4060 GPU   | 141 FPS | 3 ms                     |
| ONNX Runtime      | RTX 4060 GPU   | 93 FPS  | 6 ms                     |
| ONNX Runtime      | Intel i7 CPU   | 21 FPS  | 42 ms                    |

These performance metrics were recorded with visualization turned off, as rendering introduced a slight impact on the overall FPS. While the achieved frame rates far exceed the typical real-time threshold of 30 FPS—making them suitable for deployment in latency-sensitive applications—it's important to note that these results were obtained on a high-end RTX 4060 GPU under isolated conditions, without competing compute workloads. Real-world deployment on embedded or shared systems require further optimization to maintain consistent real-time performance.

Note: FPS is Frames processed per second, includes pre-processing, inference, post-processing, basically everything. Infer time is time taken by the model to output prediction, given an input. 

- Custom dataset - [Video](https://www.youtube.com/watch?v=UIDn_kMj-j4) - Input image stream at ~36 FPS

- CULane - [Video](https://youtu.be/uK1gyiUeAW0) - Input image stream at 1 FPS

## Conclusions

The original code includes a post-processing step that converts the model's output—typically a heatmap—into the final lane predictions. This step relies on PyTorch operations such as softmax, which are considered part of the inference pipeline and are included when measuring inference time. As a result, even with ONNX or TensorRT handling the main model inference, PyTorch operations still remain in the loop. For example, in the case of TensorRT, these post-processing steps can account for nearly one-third of the total inference time.

One key inefficiency arises from data transfers between the CPU and GPU. In the ONNX pipeline, the input image is provided as a NumPy array on the CPU, and ONNX Runtime handles GPU execution internally. However, the output is returned as another NumPy array (on CPU), which is then passed to PyTorch for GPU-based post-processing, followed by visualization on the CPU. The resulting data flow—
input (CPU) → ONNX inference (GPU) → output (CPU) → PyTorch post-process (GPU) → visualization (CPU)—
introduces unnecessary CPU-GPU transfers, adding latency and reducing the performance gains from using accelerated inference backends.

When deploying TensorRT or ONNX models on edge devices or within real-world self-driving systems, the performance dynamics change significantly compared to isolated benchmarking on a dedicated GPU. For instance, in a self-driving car, lane detection runs in parallel with other perception tasks like object detection and semantic segmentation. Simultaneously, modules for prediction, planning, and control also execute, each comprising multiple sub-tasks that may run at different frequencies and require GPU or CPU resources. This leads to contention for compute, memory, and I/O bandwidth, which can reduce the effective FPS and increase latency, even for models that perform well in isolation. Therefore, achieving real-time performance in such systems demands holistic optimization—including model compression, memory sharing, and, where possible, fusing post-processing directly into the inference engine—to ensure the full autonomy stack runs reliably and within strict latency bounds.

A more efficient and production-ready stopping point would be to integrate the post-processing logic directly into the inference engine and transition the entire inference pipeline from Python to C++. This not only reduces CPU-GPU data transfers but also eliminates the Python runtime overhead, resulting in faster and more deterministic performance—especially critical on edge devices or in real-time systems like AVs. 