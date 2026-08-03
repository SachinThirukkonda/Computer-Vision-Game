# Computer Vision Game

Workflow for creating a simple game that uses computer vision.

## Overview

Currently, the design of the game is not confirmed other than the fact that it must use some form of computer vision.

Initially, I would like to explore the capabilities of OpenCV in:

- Face detection
- Face identification
- Pose detection
- Pose classification

The aim is to produce suitably functioning programs for each of these key capabilities in order to explore the possibilities before designing the game mechanics.

---

# Face Detection

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

