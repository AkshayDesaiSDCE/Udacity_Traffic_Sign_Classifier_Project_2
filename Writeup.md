
## Writeup 

#### Data Set Summary & Exploration

###  1. Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

#### Loading the Dataset: 
The pickled files were extracted to obtain the training, validation and the test set of images 


#### Assessing the Dataset 
I used the basic pyplot and list properties to find the following dimensions: 
<br>
Number of training examples = 34799
<br>
Number of testing examples = 12630
<br>
Number of validation examples = 4410
<br>
Image data shape = [28 30]
<br>
Number of classes = 43

#### Randomly visualize an image using the random function and displayed the corresponding label

The number of images per class is displayed as a bar graph as displayed in the program file as shown below: 
<br>
X-axis --> The class number 
<br>
Y-axis --> The number of images belonging to a certain class 
![graph.JPG](attachment:graph.JPG)

### 2. How did you preprocess the Dataset 

* I first converted the images to gray scale to reduce the number of variables in the image. 
* The images were then converted from list format to a numpy array type. 
![gray_scale.png](attachment:gray_scale.png)
* The image pixel values were then normalized between -1 to 1. 
* The image datasets are then shuffled to ensure the dataset is not biased towards a particular image class. 

### 3. Describe what your final model looks like 
* The Input image of dimensions 32x32x1 is flattened and fed to the network as a 784 neuron layer
* The image is fed to convolutional layer which outputs a feature map of depth 15 by using a 5x5 filter 
* The output is activated using the relu activation function 
* The output is max pooled with a stride of 2 (width and height) to 14x14x15
* Similar steps (from 2-5) are repeated to obtain 28 and 700 feature maps in the consecutive convolutional-max_pool layers
* This 700 output is flattened and fed to 3 fully-connected layers of 200, 120 and 84 neurons respectively 
* This was then converted to the 43 neuron output layer that was returned by the function as logits. 

### 4. How did you train your model

I ran 43 Epochs while using a batch size of 100. 
<br>
The learning rate for the network was chosen at 0.0007 using an Adam Optimizer. 

### 5. Approach taken to arrive at the network architecture 

* The LeNet architecture was first tested with no change in depth of the feature map with no image normalization. The acquired validation accuracy was close to 89 percent. 
* The image was normalized without converting to gray scale and the LeNet network gave an output validation accuracy of just 5.6 percent. I thought this was due to overfitting of data. 
* After spending considerable time going through the code, it turned out that the error was due to a wrong shuffling of data. 
* After correcting this, the LeNet was able to achieve an accuracy of close to 92 percent on normalized rgb image. 
* I then tried out other network architectures such as the one suggested in the paper recommended in the project and EdleNet. 
* These architectures gave a maximum accuracy of 94 percent on the normalized RGB image. 
* I further converted the image to Gray scale and then normalized the image, while using deeper feature maps and further fully-connected layers in the network architecture. 
* I understood that the learning rate and the number of EPOCHS affects the performance of the network. 
* I realized that the modified LeNet architecture that I chose was strong in reproducing a validation accuracy of around 95 percent and fared well on the Test set. 

#### Validation Set Accuracy: 94.8 %
#### Test Set Accuraacy: 93.65 %

### 6. Test the Model on New Images 

Here are a few German Traffic Signs that I found on the web: 

![1x.png](attachment:1x.png)![2x.png](attachment:2x.png)![3x.png](attachment:3x.png)![5x.png](attachment:5x.png)![stop.png](attachment:stop.png)

The true labels for the above images in the order (top to bottom) is as follows: 

11 - Right of way at next intersection 
<br>
1 - Speed Limit (30km/h) 
<br>
12 - Priority Road
<br>
38 - Keep Right
<br>
14 - Stop 

The prediction from the netowrk for these images are as follows: 

|Probability|Prediction|
|----|----|
|0.999979|11 - Right of way|
|0.999949|1 - Speed Limit (30 km/h)|
|0.999913|12 - Priority Road|
|0.999918|38 - Keep Right|
|0.99936 |14 - Stop|

The top_k values output for the same looked as follows: 
![Capture.JPG](attachment:Capture.JPG)

### 7. (Optional) Visualizing the Network

For the 'Right of Way' sign, It is possible to see that the Network was able to break down the image to its basic components like the triangle of the sign and the basic outline of the sign itself
