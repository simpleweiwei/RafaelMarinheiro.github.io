---
layout: default
title: Scene Recognition
---

<figure>
	<img width="80%" src="/projects/scene_recognition/img/categories.png"></img>
</figure>

# Scene Recognition

This project was developed as part of an assignment of [CS6644 - Modelling the World](http://www.cs.cornell.edu/courses/CS6644/2014fa/).

## Code

The code will be available after the deadline.

## The basics

Scene Recognition is one of the core problems in Computer Vision. It can be stated in the following way: Given an image and a set of categories, we want to assign that image to the right category. To a common person, this sounds like a simple problem (see the comic). However, it is still really hard for a computer to solve it.

<figure>
	<img width="40%" src="http://imgs.xkcd.com/comics/tasks.png"></img>
	<figcaption>CS: Maybe it is even harder to explain why it is hard</figcaption>
</figure>

This problem sounds easy for a common person because that person actually solves that problem everyday. Humans are very good at recognizing images and scenes. However, we still don't know how we actually do it and we don't even know what kind of features we take into account when we try to solve it.

So far, the best idea that we had to computationally solve this problem was to divide this problem in two parts: First, we find a good feature representation of an image. After that, we will use some sample annotated images to train a classifier. After that, whenever we have a new image, we find the feature representation of that image and then we feed it to the classifier. In this project, we will use two different feature representations - Tiny Images and Bag of Sifts - and two different classifiers - Nearest Neighbors and Support Vector Machines. Nowadays, the best performing technique, the Convolutional Neural Network, still uses a similiar approach. However, it uses the image itself instead of using a low-dimensional feature representation and the classifier is much more complex than the ones that we used before.

## Feature Representation

### Tiny Image

This is a quite simple representation: Given an image, we will resize it to a 16x16 image and then we will use it as our feature representation (therefore, our feature has 256 dimensions). In our implementation, after resizing the image, we will then subtract the mean pixel value and then we normalize the vector.

### Bag of SIFT

This feature representation uses a vocabulary of SIFT features to describe the scene. Initially, given the images of the training set, we will build a "vocabulary of features" in the following way: For each image in the training set, we will sample some points in the scene. We choose a dense set and them we only pick a twentieth of those points (see the figure). Then, we compute the SIFT representation of those points and then we add them to a bag. At the end, we will have a huge number of vectors in a bag. We then try to cluster those vectors togeter in some classes using K-Means. We use 200 different classes.

<figure>
	<img width="80%" src="/projects/scene_recognition/img/vocab.jpg"></img>
	<figcaption>Building the feature vocabulary</figcaption>
</figure>

After building the vocabulary, we do the following: For each image, we choose a dense set of points and them we compute the SIFT representation of those points (see the figure). For each point, we compute the closest word and then we build a histogram of sift features. This histogram is our feature representation vector. Since we use 200 classes, then the dimensionality of our representation is 200.

<figure>
	<img width="80%" src="/projects/scene_recognition/img/sample.jpg"></img>
	<figcaption>Dense Feature Sampling</figcaption>
</figure>

## Classification

### Nearest Neighbors

This is also a pretty simple classifier. Given a vector and a set of samples, We will pick the k nearest neighbors and we will check the label of those samples. The classifier will output the label that appeared the most. In our implementation, we use k = 3.

### Support Vector Machines (SVM)

SVMs are classifiers that can be used to classify linearly separable data. If the data is not linearly separable, it will try to minimize some metric related to the misclassified points. One can also use a non-linear kernel to try to map the data to higher-dimesional spaces in which the data might be separable.

In our implementation, we use the OpenCV implementation of SVMs. We use the RBF kernel with C = 50.0 and Lambda = 50.0

## Results

### Tiny Images + KNN

We have obtained a 28.40% accuracy. The results are available [here](/projects/scene_recognition/tiny_knn).

### Tiny Images + SVM

We have obtained a 13.73% accuracy. The results are available [here](/projects/scene_recognition/tiny_svm).

### Bag of SIFT + KNN

We have obtained a 42.53% accuracy. The results are available [here](/projects/scene_recognition/sift_knn).

### Bag of SIFT + SVM

We have obtained a 61.74% accuracy. The results are available [here](/projects/scene_recognition/sift_svm).