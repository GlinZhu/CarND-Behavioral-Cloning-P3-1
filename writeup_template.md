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
* left_steering_angle=center_steering_angle +offset
* right_steering_angle=center_steering_angle +offset

-offset can be tunned and set to 0.2 in the model.

In addition to using multiple cameras, I also use data augmentation techniques to process the images to enlarge the training data set so that the model can be trained with even more data. some popular augmentation techniques are usually used in the data pre-processing such as flip, rotation, scale, and crop, etc. 
In this model, vertically flipping and cropping are used as data pre-process techniques. For example, an effective technique for eliminating background of image involves cropping and helps with choosing the area of interest. Here is an example of using cropping technique:

![Image](https://github.com/GlinZhu/CarND-Behavioral-Cloning-P3-1/blob/master/examples/images.jpg)
Center Image
![Image](https://github.com/GlinZhu/CarND-Behavioral-Cloning-P3-1/blob/master/examples/cropped%20image.jpg "Cropped image")
Cropped image
![Image](https://github.com/GlinZhu/CarND-Behavioral-Cloning-P3-1/blob/master/examples/resized%20image.jpg "Resized image")
Resized image


### Model Architecture and Training Strategy
The CNN was chosen to be the model from NVIDIA reserach work, which consists of 5 convolutional layers and 3 fully connected layers with ReLu activation. Here is the architecture:
* Input(160, 320, 3)
Images were cropped to remove the first 75 pixels (removing the sky and trees) and bottom 20 pixels (removing the car hood)

* Cropping (Removed top 75 pixels and bottom 20 pixels)

* Convolution (Kernel: 5x5, Depth: 24, Stride: 2, border: valid)

* Relu

* Convolution (Kernel: 5x5, Depth: 36, Stride: 2, border: valid)

* Relu

* Convolution (Kernel: 5x5, Depth: 48, Stride: 2, border: valid)

* Relu

* Convolution (Kernel: 3x3, Depth: 64, Stride: 1, border: valid)

* Relu

* Convolution (Kernel: 3x3, Depth: 64, Stride: 1, border: valid)

* Relu

* Flatten

* Fully Connected layer (Size: 1164, activation: Relu)

* Fully Connected layer (Size: 100, activation: Relu)

* Fully Connected layer (Size: 50, activation: Relu)

* Fully Connected layer (Size: 10, activation: Relu)

* Output (1)

Training parameters:

* Optimizer: Adam
* Learning rate: 1e-3
* Batch size: 32
* Epochs: 12
* steps per epoch:  ~270

### Validation and Results
After lot of hours of tuning and training, the model was able to successfully run at track one with no issues observed. there was no evidence of overfitting and the model was able to complete several laps since even if I tried implement dropout in the model, it doesn't make any difference on the model. The training data was split into training and validation (80/20) and used data augmentation to create more data per epoch. and I also shuffle the data before they are fed into the model.
Here is the results of validation loss from each epoch during training:

* Epoch 1/12:
272/271 [==============================] - 198s - loss: 0.0148 - val_loss: 0.0124

* Epoch 2/12:
272/271 [==============================] - 197s - loss: 0.0113 - val_loss: 0.0112

* Epoch 3/12:
272/271 [==============================] - 195s - loss: 0.0099 - val_loss: 0.0102

* Epoch 4/12:
272/271 [==============================] - 193s - loss: 0.0088 - val_loss: 0.0093

* Epoch 5/12:
272/271 [==============================] - 194s - loss: 0.0077 - val_loss: 0.0086

* Epoch 6/12:
272/271 [==============================] - 196s - loss: 0.0068 - val_loss: 0.0080

* Epoch 7/12:
272/271 [==============================] - 197s - loss: 0.0060 - val_loss: 0.0077

* Epoch 8/12:
272/271 [==============================] - 190s - loss: 0.0052 - val_loss: 0.0075

* Epoch 9/12:
272/271 [==============================] - 191s - loss: 0.0046 - val_loss: 0.0073

* Epoch 10/12:
272/271 [==============================] - 189s - loss: 0.0041 - val_loss: 0.0072

* Epoch 11/12:
272/271 [==============================] - 191s - loss: 0.0040 - val_loss: 0.0070

* Epoch 12/12:
272/271 [==============================] - 187s - loss: 0.0035 - val_loss: 0.0066

The results above show that the validation loss kept going down when model have more epoches. 

![Image](https://github.com/GlinZhu/CarND-Behavioral-Cloning-P3-1/blob/master/examples/Model_validation_loss.png)

### Simulation
I was able to train the model on track one and it successfully runs on the track one without any issues, the video shows below:

