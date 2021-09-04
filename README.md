# CuriosityClassifier
Semi-supervised labeling of Mars images shot by the Curiosity Rover using an Auto Encoder and a SVM
Inspired from [this](https://arxiv.org/pdf/1911.06623.pdf) paper I found on Arxiv.

# **Introduction**

The Curiosity Rover stands strong on Mars, performing scientific experiments and sending images back on a regular basis. Broadly speaking, these images fall into 25 categories, including but not limited to "wheel", "drill", "drill hole", "turret", etc. Labelling all the images taken by the rover is a laborious task, though. From around 32k images shot by the rover, we only have labels for 6.6k of them (~20%). Given that about a fifth of the images have been labelled, we could attempt to train a Deep Neural Network for labelling the remaining images.


Unfortunately, since we have 25 image classes, that averages out to us having only about 250 images per class. This makes training a normal CNN for image classification very difficult, even through means of data augmentation.


Hence, we can try using semi-supervised learning methods to train a classifier. We leverage the original 32k images to train an AutoEncoder that attempts to learn a lower-dimensional representation of the images (aka latent vector). We subsequently make use of the lower-dimensional representation of the images to train a classifier. Given that we're dealing with vectors, we can use K-Nearest Neighbours and Support Vector Machines to build the classifier.

So, our training process is as follows:

1. Train a convolutional auto encoder on all 32k images.
2. Get latent vectors for all 6.6k labelled images.
3. Train a classifier on the 6.6k latent vectors.

**NOTE :**
This is only possible for this problem statement, because all our images are captured from the same source (Curiosity's camera). This procedure might not necessarily be valid for other datasets.

## **Results**
After training the autoencoder for 150 epochs and training the classifier on the image latent vectors, we get
- KNN : 92.1% accuracy
- SVM : 94.5% accuracy
