# Final Project: Classification and Detection with Convolutional Neural Networks
The goal of this project is to design a digit detection and recognition system which takes in a single image and returns any sequence of digits visible in the image by using convolution neural networks.

## Getting Started
Please follow the instructions on how to get the code running.
First, download the all project files to your local machine.
Second, get the corrected environment installed, tensorflow-gpu=1.12.0, python=3.6.7, keras=2.2.4 are used in the project.


1. Download the all project files from gradescope into your testing directory
2. Download the vgg model from [GT Box](https://gatech.box.com/shared/static/z4jy5rit7bft4j047926mxf2m3wy14zr.h5) or [Dropbox](https://www.dropbox.com/s/ejeqtum3auqgp2k/vgg16_best_model.h5?dl=0)
3. Put the vgg model under your testing directoy(for example, ./cv_final_proj)
4. cd ./your_testing_directoy, where all projects files are stored
5. conda env create -f mycv_proj.yml
6. conda activate cv_proj
7. python run.py

## Project folder structure
* Test_images folder - contains all test images for this project, 1-6.png
* graded_images folder - contains processed images
* digit_detector.ipynb - my own designed CNN model implemented in tensorflow
* vgg16_classifier.ipynb - VGG16 pre-trained model implemented in Keras
* data_process.py
* cnn_classifier.py - CNN model inference file
* vgg_classfier.py - VGG16 inference file
* run.py - main file to run the classifier
