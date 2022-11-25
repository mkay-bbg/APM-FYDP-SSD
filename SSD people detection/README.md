# Person-Detection-and-Tracking

## Introduction
The Project is based on Person Detection and tracking and I am mainly focusing on the Person tracking. As shown in the output gif in the README.md or the output.mp4 each person will be provided with an `id` as soon as he enters a frame and the `id` is maintained regardless of the detection happening in concurrent frames. The algorithm does Person Detection and tracks him as long as he remains in the frame.

## Output
![Alt Text](https://github.com/ambakick/Person-Detection-and-Tracking/blob/master/person%20detection%20and%20track.gif)


## For executing
### Run Person_det_track.py
Person_det_track.py detects and tracks the person using SSD and Kalman Filter

## Requirements
Please try to Stick on with the version provided as much as possible other-wise you will face compatibility issues. I have used the best combination possible during the time of coding.
* **opencv [v3.1]**
	* **Installation in linux:**
			For a complete installation of opencv in ubuntu you can refer [here](http://www.pyimagesearch.com/2015/06/22/install-opencv-3-0-and-python-2-7-on-ubuntu/).
	* **Installation in windows**
			For a complete installation of opencv in windows you can refer [here](https://putuyuwono.wordpress.com/2015/04/23/building-and-installing-opencv-3-0-on-windows-7-64-bit/)
      
* **Tensorflow [v1.5.0]** 
	* **Installation**
		Tensorflow has amazing documentation [here](https://www.tensorflow.org/install/pip)
## Methodology / Approach
The method Proposed here is divided into 2 main parts

* Person Detection - The person detection in Real-time is done with the help of Single Shot MultiBox Detector. SSD achieves 75.1%
	mAP, outperforming a comparable state of the art Faster R-CNN model. and the SSD model is available in the Tensorflow detection
	zoo. The seamless integration of SSD with tensorflow helps in further optimization and implementation of the algorithm.
	The SSD object detection composes of 2 parts:
	* Extract feature maps, and 
	* Apply convolution filters to detect objects.
	Even though SSD is capable of detecting multiple objects in the frame, in this project I limited its detection to just a human.

* Person Tracking - Bounding box can be achieved around the object/person by running the Object Detection model in every frame, but this is computationally expensive.
	The tracking algorithm used here is Kalman Filtering . The Kalman Filter has long been regarded as the optimal solution to many tracking and data prediction tasks. Its use in the analysis of visual motion. The purpose of Filtering is to extract the required information from a signal, ignoring everything else. In this project, the Kalman Filter is fed with the velocity, position and direction of the person which helps it to predict the future location of the Person based on his previous data.

The tracking part still faces some problems at the time of occlusion. (Working on it)

## Performance of Code
* The code was run on both CPU and GPU:	
	* Nvidia Quadro 4000  -  ~30FPS
	* Nvidia Jetson TX2   -  ~20FPS
	* Intel i5 CPU	      -  ~10FPS

## Overview / Usage
The system consists of two parts first, human detection, and secondly tracking. Early research was biased toward human recognition rather than tracking. Monitoring the movements of a human being raised the need for tracking. Monitoring movements are of high interest in determining the activities of a person and the attention of a person.

Reducing the computation power requirement - A normal objection detection algorithm detects the Object but does not track (assign an Id) an Object across frames; thus has to be run in every frame to get the bounding box. Tracking will help to reduce the number of
times the Detection algorithm has to be run, i.e, instead of running the Detection algorithm every frame, this implementation runs detection every 5 frames.

Object Detection model failure compensation - there might be some poses where SSD may not detect the person. Even occlusion can affect the detector significantly; that is where the tracking algorithm can greatly help us.

Identity retrieval - Tracking of a human being can be used as a prior step in biometric face recognition. Keeping continuous track of a person will allow identifying a person at any time. Even if face identification is not possible at a particular set of frames, his identity can be found tracking.
By Neeraj Menon
