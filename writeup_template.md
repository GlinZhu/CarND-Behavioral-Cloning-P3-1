# **Behavioral Cloning Project** 

## Writeup Report

## Overview
The entire goal of this project is to train the Convoluntional Neural Network(CNN) to predict the steering angle based on the given training data. The car in the simulator was equipped with three cameras which are able to provide left, center and right images of road conditions. By giving the training data, the CNN model was trained and able to generate the steering commands from the video images of three cameras. This problem turns out to be a regression task which is different from traditional classification task. 

The goals / steps of this project are the following:
* Use the simulator to collect data of good driving behavior
* Build, a convolution neural network in Keras that predicts steering angles from images
* Train and validate the model with a training and validation set
* Test that the model successfully drives around track one without leaving the road
* Summarize the results with a written report

## Proposed Solution
### Data Collection
Traning data was collected on simulator and two laps of track 1 as well as recovery data were collected, since the first time when I train the model with normal on center driving data, the car truns out to be driving outside of the road especially when it's trunig on the curve, and can't recover by itself, therefore, I collected more recovery data while the vehicle encounters turning curve. 

### Data processing and augmentation
images from three cameras are all used in the model training, however, the image taken from side cameras are different from the ones that are taken from center camera, the steering angles for side cameras need to be adjusted since from the perspective of left camera, the steering angle command will be less than steering angles from center camera, and from the right camera's perspective, the steering angle would be larger than the angle from the center camera. therefore, to account for being off center, I adjust the steering angles for the images taken from side cameras as fllows:
*left_steering_angle=center_steering_angle +offset
*right_steering_angle=center_steering_angle +offset

-offset can be tunned and set to 0.2 in the model.

In addition to using multiple cameras, I also use data augmentation techniques to process the images to enlarge the training data set so that the model can be trained with even more data. some popular augmentation techniques are usually used in the data pre-processing such as flip, rotation, scale, and crop, etc. 
In this model, vertically flipping and cropping are used as data pre-process techniques. For example, an effective technique for eliminating background of image involves cropping and helps with choosing the area of interest. Here is an example of using cropping technique:

### Model Architecture and Training Strategy




