# German Sign Classifier (Assignment-2)
---

## 1) Description of the pipeline
---

The pipeline can be described in the following phases:- 

1) Data gathering

2) Data exploration

3) Preprocessing

4) Model Design

5) Model Training and Validation Accuracy

6) Test Accuracy

7) Looking at performance and softmax probabilities for new images

8) Visualizing the output

---

The individual steps of the pipeline are explained below:-

---

### 1) Data gathering

I have downloaded the data from the official dataset provided [here](https://d17h27t6h515a5.cloudfront.net/topher/2017/February/5898cd6f_traffic-signs-data/traffic-signs-data.zip).

I have loaded the pickle files for the datasets after which the number of samples in training, validation and testing are:-

Training:- 34799
Validation:- 4410
Testing:- 12630

All images are three channel RGB images each of which has a dimension of 32,32.

---

### 2) Data exploration

I looked at many sample images from our training set to get an intuition of what I am dealing with. Here are a few sample images:-

![Alt text](./markup_images/example1.png?raw=true "Title")
![Alt text](./markup_images/example2.png?raw=true "Title")
![Alt text](./markup_images/example3.png?raw=true "Title")

I also plotted a histogram of training labels to see how many examples from each class do we have.

![Alt text](./markup_images/histogram_original_labels.png?raw=true "Title")

We can clearly see that this is quite an unbalanced histogram. This is a problem that I have tried to address later.


---
### 3) Preprocessing

I have done the following three steps as part of preprocessing:-

1) To address the problem of unbalanced classes that we saw above, the first thing that I have done is create additional data for classes which have very few data points. I have rotated the images of existing data in these classes randomly from +30 degrees to -30 degrees in order to achieve that. I have ensured that each class should at the least have as many images as the mean images of the original classes. This has resulted in a much more balanced dataset. The histogram for this is present below:-

![Alt text](./markup_images/balanced_histogram.png?raw=true "Title")

2) Converting the image to grayscale since shape is a more important characteristic here than color of the signs. I had experimented earlier on with training my model with 3 channels but it wasn't really leading to much higher accuracy so I converted to grayscale. Here's how a sample image looks after conversion to grayscale:-

![Alt text](./markup_images/color.png?raw=true "Title")
![Alt text](./markup_images/b&w.png?raw=true "Title")
 
3) Normalization - I have scaled down all values from a range of 0.1 to 0.9 as taught in the lessons to normalize the data. Using 0.1 as a starting point instead of 0 helps getting some activations even for small values.

---

---
### 4) Model Design

I have used the standard lenet model taught in the class and made a few adjustments to it:-

1) Used 43 outputs instead of 10.
2) Added dropout to avoid overfitting of data - This was resulting in better validation accuracy.
3) Used tanh activations instead of relu - This was resulting in better validation accuracy.

Here is a description of the model

![Alt text](./markup_images/network_description.png?raw=true "Title")


---

### 5) Model training and validation

I used several values of epochs and batch_size and found that a batch size of 16 and 30 epochs were giving most optimal accuracy and worked well within reasonable training time.

I achieved a validation accuracy of upto 95.6%.

---

### 6) Model test accuracy

After tuning, the model was final tested for accuracy on the test data. Here, we achieved a test accuracy of 93.5%.

---

### 7) Looking at performance and softmax probabilities for new images

I acquired 5 images from the wikipedia page of german signs. The model was able to classify 4 of them correctly i.e. 80% accuracy. Although given that these were clean images, I was hoping for a 100% accuracy in this.

It wasn't able to classify the image with 60 Km/hr sign.

The images I have taken are fairly well standardised and should be reasonably easily to classify. The network is being able to classify shapes like bumpy road but is having a hard time differentiating between the numbers. The 60 km/hr image is being confused with 50 and 40km/h. Although digit recognition is a fairly well solved problem in the context of deep learning, it might not be working well here because the network hasn't specifically bein given data on numbers only.

Looking at the softmax probability, I saw that 60km/hr was within the top3 predictions for this image.



### 8) Visualizing the network

I looked at the first convolutional layer and its activation to understand what the neural network is learning.

#### Input image:-

![Alt text](./markup_images/bumpy_road.png?raw=true "Title")

#### First Convolutional Layer

![Alt text](./markup_images/conv_layer.png?raw=true "Title")


#### Tanh Activation 

![Alt text](./markup_images/tanh_layer.png?raw=true "Title")

The model seems to be learning basic features like lines and curves since they are exaggerated in these pictures above.

The three edges of the triangle are very clearly detected by the network possibly because it would have seen these in many examples. 

We can also see some level of contrast increasing as we go from conv_layer to tanh layer which is possibly due to activation function.






---