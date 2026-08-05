# Computer Vision Game

Workflow for creating a simple game that uses computer vision.

## Overview

Currently, the design of the game is not confirmed other than the fact that it must use some form of computer vision.

Initially, I would like to explore the capabilities of OpenCV in:

- Face detection
- Face recognition
- Pose detection
- Pose classification

The aim is to produce suitably functioning programs for each of these key capabilities in order to explore the possibilities before designing the game mechanics.

---

<details>
<summary><h1>Face Detection</h1></summary>

## YuNet

For facial detection, I chose to work with **YuNet**.

YuNet is a Convolutional Neural Network (CNN)-based pretrained facial detection model. Its main advantages are:

- It is within the OpenCV ecosystem, simplifying the overall pipeline.
- It is open source.
- It provides efficient real-time face detection.

The model achieves:

- **0.834 AP_easy**
- **0.824 AP_medium**
- **0.708 AP_hard**

on the WIDER Face validation set.

The pretrained model is available through the OpenCV Zoo repository on GitHub.

---

## Pipeline

### Initialisation

1. Initialise webcam as the input source.
2. Initialise the `VideoWriter` object:
   - Frame rate
   - Frame size
   - Codec
   - Output filename
3. Configure the output video window.
4. Load the YuNet face detection model:
   - Download pretrained model weights (`.onnx` file).
   - Initialise the YuNet detector.
5. Set the model input size.

### Processing Loop

For each frame:

1. Read frame and validate input.

2. **Model-specific operations**
   
   - Prepare frame input for the model.
   - Run face detection.

   > Note: YuNet only requires the input size to be set. This is fixed for the webcam stream and is therefore configured outside the processing loop.

3. **Application logic**

   - Process detection results.
   - Draw annotations.
   - Display frame.
   - Save frame.
   - Check for exit condition (e.g. key press).

### Cleanup

Release resources:

- Release webcam input.
- Release `VideoWriter`.
- Close display windows.

</details>

<details>
<summary><h1>Face Recognition</h1></summary>

## SFace Face Recognition

For face recognition, I chose to work with **SFace**.

SFace is a pretrained deep learning face recognition model that works by extracting a feature embedding, which is a high-dimensional vector that encodes distinguishing features of the face. These face embeddings can then be compared using similarity metrics such as cosine similarity or L2 distance to recognise the same person between images.
Its main advantages are:

- It is within the OpenCV ecosystem, simplifying the overall pipeline.
- It builds upon face detection using YuNet
- It is open source.

There are three models available, achieving:

- **SFace       0.9940**
- **SFace block	0.9942**
- **SFace quant	0.9932**

While the baseline model boasts the highest accuracy, since the model's weights are stored in a higher precision format (FP32) while the quantized counterparts use a less precise INT8 format, the quantized variants are said to be 2-4× faster. The greater speed is ideal for webcam face recognition, however, I have decided to test the capabilities of all three models.

The pretrained model is available through the OpenCV Zoo repository on GitHub.

---

## Pipeline

### Initialisation

1. Initialise webcam as the input source.
2. Configure the output video window.
3. Initialise the `VideoWriter` object:
   - Frame rate
   - Frame size
   - Codec
   - Output filename
4. Load the YuNet face detection model:
   - Download pretrained model weights (`.onnx` file).
   - Initialise the YuNet detector object.
5. Load the SFace face recognition model:
   - Download pretrained model weights (`.onnx` file).
   - Initialise the SFace recognition object.
5. Set the model input size.

### Processing Loop

For each frame:

1. Read frame and validate input.

2. **YuNet Model-specific operations**
   
   - Prepare frame input for the model.
   - Run face detection.

   > Note: YuNet only requires the input size to be set. This is fixed for the webcam stream and is therefore configured outside the processing loop.

3. Run face recognition on each face

4. **Application logic**

   - Process detection and recognition results.
   - Draw annotations.
   - Display frame.
   - Save frame.
   - Check for exit condition (e.g. key press).

### Cleanup

Release resources:

- Release webcam input.
- Release `VideoWriter`.
- Close display windows.
</details>

