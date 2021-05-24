# ONNX Runtime Inference

## Introduction

ONNX Runtime C++ inference example for image classification using CPU and CUDA.

## Dependencies for CUDA 10.2

* CMake 3.16.8
* ONNX Runtime 1.6.0
* OpenCV 4.5.0

## Dependencies for CUDA 11.2

* CMake 3.16.8
* ONNX Runtime 1.7.2
* OpenCV 4.5.2

## Usages

### Build Docker Image

```bash
$ docker build -f docker/onnxruntime-cuda.Dockerfile --no-cache --tag=onnxruntime-cuda:1.6.0 .
```

### Build Docker Image for CUDA 11.2

```bash
$ docker build -f docker/onnxruntime-cuda11.Dockerfile --no-cache --tag=onnxruntime-cuda11:1.7.2 .
```

### Run Docker Container

```bash
$ docker run -it --rm --gpus device=0 -v $(pwd):/mnt onnxruntime-cuda:1.6.0
```

### Run Docker Container for CUDA 11.2

```bash
$ docker run -it --rm --gpus device=0 -v $(pwd):/mnt onnxruntime-cuda11:1.7.2
```

### Build Example

```bash
$ cmake -B build
$ cmake --build build --config Release --parallel
```

### Run Example

```bash
$ cd build/src/
$ ./inference  --use_cpu
Inference Execution Provider: CPU
Number of Input Nodes: 1
Number of Output Nodes: 1
Input Name: data
Input Type: float
Input Dimensions: [1, 3, 224, 224]
Output Name: squeezenet0_flatten0_reshape0
Output Type: float
Output Dimensions: [1, 1000]
Predicted Label ID: 92
Predicted Label: n01828970 bee eater
Uncalibrated Confidence: 0.996137
Minimum Inference Latency: 7.45 ms
```

```bash
$ cd build/src/
$ ./inference  --use_cuda
Inference Execution Provider: CUDA
Number of Input Nodes: 1
Number of Output Nodes: 1
Input Name: data
Input Type: float
Input Dimensions: [1, 3, 224, 224]
Output Name: squeezenet0_flatten0_reshape0
Output Type: float
Output Dimensions: [1, 1000]
Predicted Label ID: 92
Predicted Label: n01828970 bee eater
Uncalibrated Confidence: 0.996137
Minimum Inference Latency: 0.98 ms
```

## References

* [ONNX Runtime C++ Inference](https://leimao.github.io/blog/ONNX-Runtime-CPP-Inference/)
