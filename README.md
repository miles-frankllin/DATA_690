# Final Project for DATA 690, Spring 2021

# Requirements
- Google Colab
- [labelImg](https://github.com/tzutalin/labelImg)
- [Kaggle Account](https://www.kaggle.com/)


## Libraries
- os
- re
- sklearn
- keras
- pandas
- shutil
- time
- PIL
- IPython
- base64

# Motivation
Initially, I wanted to develop a facial recogntition model that would dynamically change the desktop windows, 
depending on who was detected in the frame. While I had trouble deploying the model in a way that allowed me to 
interact with my desktop applications (see Difficulties section), I was able to successfully train a facial 
recognition model.  

# Data
I captured images, of myself (Miles), and my partner (Sid) to serve as the two classes for classification.
Images were capture using the OpenCV library, and dynamically named in the images folder for ease. Next, the images were hand labeled
using the [labelImg](https://github.com/tzutalin/labelImg) tool, and saved in the annotations folder.
In the annotations folder, filenames had the same name as the image they were annotating, with the .jpeg extension replaced with a .xml extension.
Finally, the data was saved into a Kaggle folder, for ease of access in Google Colab notebook.

# Model
I followed [Step by Step: Build Your Custom Real-Time Object Detector](https://towardsdatascience.com/custom-real-time-object-detection-in-the-browser-using-tensorflow-js-5ca90538eace) 
guide on Towards Data Science, and used a pre-trained SSD MobileNet V2 Object Detection model as the base model for this model. Google 
Colab was used in place of Jupyter Notebook to make use of the free storage space provided. This was particularly helpful, as I am currently near 90%
of my local storage capacity, and experience performance difficulties whenever I occupy storage above this threshold.  

# Results 
While I still need to quantify the accuracy of the model, it appears to perform well on the entirety of the testing set images (sample outputs below).
Moving forward, I will implement a notebook to score using mean precision Mean Average Percentage Error(MAPE). In short, this method evaluates 
compares the area of the predicted region against the true are of the target image.

# Difficulties
Per the motivation, I initially wanted to design a model that would dynamically change the desktop windows, 
depending on who was detected in the frame. I was able to do this in a clunky manner, using the haarcascade frontal face object detection model from openCV,
and then ran a classification CNN model on the image if a face was detected. This had some success, although there were some serious drawbacks as well. For one, 
this method only allowed me to assign one class to an image, regardless of the number of people present in the photo. Another issue was that if the 
initial model picked up noise, the second model had to classify the image, as if there was actually a picture in the frame. This made it difficult to 
design the application logic, that dynamically adjusted the desktop as intended.

Moving the application into Google Colab came with some advantages, and disadvantages as well. First, this change made it much easier to use the
Tensorflow Object Detection API while making use of free disk space for training the model. However, Google Colab is not compatible with OpenCV, and requires
detailed understanding of JavaScript to control the camera from the Colab Notebook (of which I do not have at this time). This made it difficult to stream the camera feed into the model, and show the detected boxes within the Google Colab notebook.

# Resources
- [Tensorflow Object Detection API Tutorial](https://blog.tensorflow.org/2021/01/custom-object-detection-in-browser.html)
- [Tensorflow Object Detection API Tutorial Colab Notebook](https://colab.research.google.com/drive/1MdzgmdYJk947sXyls45V7auMPttHelBZ?usp=sharing)
- [LabelImg](https://github.com/tzutalin/labelImg)
- [Scoring Model](https://www.kdnuggets.com/2021/03/evaluating-object-detection-models-using-mean-average-precision.html)

