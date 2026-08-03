# Computer-Vision-Game
Workflow for creating a simple game that uses computer vision

Currently, the design of the game is not confirmed other than the fact that it must use some form of computer vision. Initially, I would like to explore the capabilities of OpenCV in: detecting faces, identifying faces, pose detection, and pose classification. I aim to produce suitably functioning programs for each of these key capabilities, in order to get the ball rolling, before designing the game aspect.

Face Detection
For facial detection, I chose to work with YuNet. YuNet is a Convolutional Neural Network (CNN)-based pretrained facial detection model. Its main advantages are that it is within the OpenCV ecosystem, which simplifies the pipeline, and that it is open source. The model achieves 0.834(AP_easy), 0.824(AP_medium), 0.708(AP_hard) on the WIDER Face validation set. The pretrained model is found in the OpenCV Zoo repository on GitHub



Pipeline:
Initiation
    Load face detection YuNet model - download model parameter weightings .onnx file from GitHub
    Initialise webcam as input source
    Initialise VideoWriter object - provide fps, frame size, codec, and name of output video file
    Configure output video window
Start processing loop
    Read frame and validate
    Model-specific Operations
        Preprocess frame for the model - convert into blob, adjusting scaling, mean, colour  channel convention, and cropping #the only preprocessing required was to set input size, which is fixed so was completed outside of the preprocessing loop
        Run face detection
    Application Logic
        Process results
        Draw annotations
        Display frame
        Save frame
        Check for exit condition (e.g. check key press)
Release resources

