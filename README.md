# Traffic-Sign-Classifier

Build a Traffic Sign Recognition Project

The goals / steps of this project are the following:

* Load the data set (see below for links to the project data set)
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images
* Summarize the results with a written report


# Data Set Summary & Exploration

1. Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

This section is explained in the Jupyter notebook file included in the repository. 

2. Include an exploratory visualization of the dataset.

This section is explained in the Jupyter notebook file included in the repository.

# Design and Test a Model Architecture

1. Describe how you preprocessed the image data. What techniques were chosen and why did you choose these techniques? Consider including images showing the output of each preprocessing technique. Pre-processing refers to techniques such as converting to grayscale, normalization, etc. (OPTIONAL: As described in the "Stand Out Suggestions" part of the rubric, if you generated additional data for training, describe why you decided to generate additional data, how you generated the data, and provide example images of the additional data. Then describe the characteristics of the augmented training set like number of images in the set, number of images for each class, etc.)

The images are shown in the jupyter notebook file. The colors for this project are not necessary although there is important information that is lost I decided to mimic the Lenet lab architecture which requires the input of 32x32x1. 

As a first step I decided to convert the images to grayscale becuase I uncovered if I do the normalization first it lowers the acuracy of the model during the training process. When I switched back to grayscaling first, that improved considerably the accuracy of the model. 

As a second step I do the normalization so the data has mean zero and equal variance. 

2. Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

I started with just copying the same architecture from the Lenet Lab, and that is why I decided grayscaling and normalizing my datasets as first step (to be able to use the same architecture). This model however didn't work as expected for some reason, I was starting with very low validation accuracy of 0.39 for the first EPOCH and increasing to 0.8 for the last EPOCH. Then I implemented the Lecun classifier from the papaer which has the Inception module and that imporved a lot the accuracy by 25%. The layers as follows: 

a) Input grayscale images (32x32x1)
b) 5x5 convolution (32x32x1 in, 28x28x6 out)
c) Relu
d) 2x2 max pooling (28x28x6 in, 14x14x6 out)
e) 5x5 convolution (14x14x6 in, 10x10x16 out)
f) Relu
g) 2x2 max pooling (10x10x16 in, 5x5x16 out)
h) 5x5 convolution (5x5x6 in, 1x1x400 out)
i) Relu
j) Flatten layers (1x1x400 -> 400) and (5x5x16 -> 400)
k) Concatenate flattened layers to a single size 800 layer
l) Dropout layer
m) Fully connected layer (800 in, 43 out)
n)logits

3. Describe how you trained your model. The discussion can include the type of optimizer, the batch size, number of epochs and any hyperparameters such as learning rate.

I used the Adam optimizer (same from the LeNet lab), see the hyerparameters listed below:
epochs: 40
batch size: 128
rate: 0.0009
mu: 0
sigma: 0.1
dropout keep probability for training: 0.5
dropout keep probability for evaluate: 1.0

4. Describe the approach taken for finding a solution and getting the validation set accuracy to be at least 0.93. Include in the discussion the results on the training, validation and test sets and where in the code these were calculated. Your approach may have been an iterative process, in which case, outline the steps you took to get to the final solution and why you chose those steps. Perhaps your solution involved an already well known implementation or architecture. In this case, discuss why you think the architecture is suitable for the current problem.

As mentioned in the previous paragraph my first approach was to mimic the Lenet Lab architecture then I switched to Lecun without knowing the impact of normalizing before grayscaling. It took me a long time to realize changing the processing image sequence (grayscaling then normalizing and not the ther way) would impact on the validation accuracy and by then the Lecun was already implemented so my guess is Lenet would have also worked well if I had noticed this before implemented lecun. I also played a lot with the hyperparameters and ended up using 40 EPOCHS and 128 batch size, and as far as the learning rate I found out that 0.0009 is in general more realiable and stable than 0.001. 

# Test a Model on New Images

1. Choose five German traffic signs found on the web and provide them in the report. For each image, discuss what quality or qualities might be difficult to classify.

This part is explained in the Jupyter notebook file. 

2. Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. Identify where in your code predictions were made. At a minimum, discuss what the predictions were, the accuracy on these new predictions, and compare the accuracy to the accuracy on the test set (OPTIONAL: Discuss the results in more detail as described in the "Stand Out Suggestions" part of the rubric).

This part is explained in the Jupyter notebook file. The model however predicted the image with 100% accuracy. 

3. Describe how certain the model is when predicting on each of the five new images by looking at the softmax probabilities for each prediction. Provide the top 5 softmax probabilities for each image along with the sign type of each probability. (OPTIONAL: as described in the "Stand Out Suggestions" part of the rubric, visualizations can also be provided such as bar charts)

This part is explained in the jupyter notebook file. 






