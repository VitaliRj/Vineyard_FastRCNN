# Vineyard_FastRCNN

## Introduction
![Image of Promo](/media/Promo.png)

This project presents an object/obstacle detector using a Fast Region-based Convolutional Network method (Fast R-CNN) in an agricultural environment using Matlab. 

Convolutional Neural Networks have significantly improved image classification and detection accuracy in recent years [1]. Especially complex scenes and objects with a high variety of optical features and surfaces can be detected with increasing confidence.  Agriculture is a brilliant example for heterogenous geometries and surfaces that introduce innumerable difficulties for traditional computer vision approaches.

![Image of plant_diversity.png](/media/plant_Diversity.png.png)

Having a look into modern vineyards, a progressively common method of weed control is to mechanically/physically remove weed beneath the plants. Hence the implement, removing the weed, has to detect the plants and other obstacles to avoid collisions. The state of the art is to “feel” if there is an obstacle in front of the implement as shown here:
![Image of contactSensor](/media/contactSensor.png)

https://www.youtube.com/watch?v=5lbuL1qP2mc

This physical interaction can damage the plants bark, thus allowing fungus to grow. Additional benefits of having a contactless system can be:

* Data mining for smart farms,
* Autonomous systems,
* Health monitoring.

## Increased Complexity of Modern Networks
The increased complexity and size of resent CNNs like VGG16, VGG19, GoogleNet or the Inception networks resulted in a high processing power demand for classification/detection. While this growing demand is manageable on large server farms of Amazon and Google, embedded solutions still depend on efficient image processing algorithms. Over the next years the “autonomous driving” industry will demand more low-cost embedded systems and manufactures like NVIDIA [2] will push aggressively into the ECU market that is now dominated by e.g. BOSH [3]. 

Let’s hope the competition results in better and more affordable products.  Until then, the algorithms have to be optimized to run on embedded systems with limited processing capabilities.

## The Network
Having a wide variety of pretrained CNNs I choose the VGG-19 Series network as a base for this project [4]. The network comes with the following layers:

* 1   'input'     Image Input             224x224x3 images with 'zerocenter' normalization
* 2   'conv1_1'   Convolution             64 3x3x3 convolutions with stride [1  1] and padding [1  1]
* 3   'relu1_1'   ReLU                    ReLU
* 4   'conv1_2'   Convolution             64 3x3x64 convolutions with stride [1  1] and padding [1  1]
* . . .
* 37   'relu5_4'   ReLU                    ReLU
* 38   'pool5'     Max Pooling             2x2 max pooling with stride [2  2] and padding [0  0]
* 39   'fc6'       Fully Connected         4096 fully connected layer
* 40   'relu6'     ReLU                    ReLU
* 41   'drop6'     Dropout                 50% dropout
* 42   'fc7'       Fully Connected         4096 fully connected layer
* 43   'relu7'     ReLU                    ReLU
* 44   'drop7'     Dropout                 50% dropout
* 45   'fc8'       Fully Connected         1000 fully connected layer
* 46   'prob'      Softmax                 softmax
* 47   'output'    Classification Output   crossentropyex with 'tench', 'goldfish', and 998 other classes 

as shown in [4].

Note: The input layers and the last nine layers were modified to increse the performance and fit the needs of this project.

The algorithm, chosen for the training of the new network was the Fast-RCNN approach presented in [5]. This algorithm is already implemented in MATLAB and is a part of the Computer Vision System Toolbox. 


[1] Girshick, Ross. "Fast r-cnn." Proceedings of the IEEE International Conference on Computer Vision. 2015.

[2] https://www.nvidia.com/en-us/self-driving-cars/

[3] https://markets.businessinsider.com/news/stocks/automated-driving-in-cities-daimler-and-bosch-select-nvidia-ai-platform-1027356557

[4] https://de.mathworks.com/help/nnet/ref/vgg19.html
