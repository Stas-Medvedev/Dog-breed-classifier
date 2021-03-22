[//]: # (Image References)

[image1]: ./sample_outputs/dog2.jpg "Sample output"
[image2]: ./sample_outputs/human1.jpg "Sample output"
[image3]: ./sample_outputs/Godzilla.jpg "Sample output"


## Project Overview

The algorithm in this project identifies the breed of a dog in a given image. It can also detect human faces, and if it receives a picture of a human, it returns the resembling breed. Here are a couple of sample outputs:  

![Sample Output][image1]	![Sample Output][image2]

## Datasets

The datasets used in the project can be downloaded from the following links: [dog dataset](https://s3-us-west-1.amazonaws.com/udacity-aind/dog-project/dogImages.zip) (.zip file) and [human dataset](http://vis-www.cs.umass.edu/lfw/lfw.tgz) (.tgz file).

## Implementation

The algorithm has several parts with the following workflow:
- Dog detector checks the input image for dogs
  - If a dog is found, the dog breed classifier checks the image and returns the most likely breed, and the app run ends
  - If no dog is found, the image goes to the human face detector
- Face detector checks the image
  - If an image is detected, the dog breed classifier checks the image and return the most likely breed, and the app run ends
  - If no human is detected, the app displays a message as in the sample below, and the app run ends  
![Sample Output][image3]

### Dog detector
The dog detector uses the pre-trained VGG-16 network to predict the overall contents of the input image. If the predicted class is between 151 and 268, which are the various breeds that VGG-16 can identify, the dog detector marks the image as containing a dog.

### Face detector
The face detector uses a Haar feature-based cascade classifier through OpenCV.

### Breed classification
There were two approaches to classify the breeds, both of which used convolutional neural networks (CNN) coded with PyTorch.  

The first approach was to build and train a CNN from scratch. That resulted in a CNN that classified the breeds with 13% accuracy.

The second approach was to use the transfer learning method and fine-tune a pre-trained CNN. I initially tried the VGG-19 and the ResNet-50 networks in this approach, which produced about 76% accuracy for both models. I then attempted it with the ResNet-101 network and a modified set of dataloaders, and the model achieved 87% prediction accuracy on the test set.
