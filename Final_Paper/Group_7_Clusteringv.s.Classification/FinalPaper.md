# Machine learning: Clustering v.s. Classification
## By: Jiayang Bao, Mijia Ma, Sky Li | Team 7 Beng183 Fall 2022

<br>

# Table of contents <a name="tob"></a >
- [Overview](#overview)
- [Simple kNN Application Example in Bioinformatics](#kNN)
- [Clustering v.s. Classification](#3)
- [K-nearest-neighbors classification (KNN)](#4)
  - [Intuition](#4.1)
  - [Implementation](#4.2)
  - [Distance metrics](#4.3)
  - [Normalization](#4.4)
  - [Importance of K](#4.5)
- [Summary](#5)


# Overview 💻 <a name="overview"></a >
[BACK TO TABLE OF CONTENTS](#tob)

<p align="center" width="100%">
<img src="https://user-images.githubusercontent.com/97704603/205791858-a5bfc0ca-7473-4f0a-ab87-6ee47877c7ae.png" width=70% height=70%>
<p>
  
###### From https://www.youtube.com/watch?v=ukzFI9rgwfU&t=6s

As humans, we learn from our past experiences and thus could better adjust our performances in the future. 
The first time you have a dinner in a new restaurant, the experience you had in the restaurant would 
influence whether or not you will choose the restaurant again. 
For machines, they are developed and given instructions by humans to help perform some tasks. 
Calculators can be used to help us figure out the square root of an extremely large number. 
For simple tasks like calculating the square root of a number, humans can explicitly program the command. 
However, for advanced tasks, it may be hard for humans to efficiently create the needed algorithms to be put in the machines. 

> ### Machine learning is a method of data analysis that automates analytical model building.  

Here is when **machine learning** comes in handy. **Tasks can be performed by machine learning programs without being explicitly programmed to do. 
Machines learn from the data provided** (Wink-wink, we will talk about details of different datasets later in this chapter) and then perform certain tasks. 
**In Bioinformatics**, application of machine learning algorithms include **genomics, proteomics, microarrays, systems biology, evolution, and text 
mining**.
  
<p align="center" width="100%">
<img src="https://user-images.githubusercontent.com/97704603/205791233-9f680b86-0e11-4644-8e39-b919d1d7e785.png" width=70% height=70%>
<p>
  
###### Generated from https://monkeylearn.com/word-cloud/
  <br>
  
---
  
# Simple kNN Application Example in Bioinformatics <a name="kNN"></a >
[BACK TO TABLE OF CONTENTS](#tob)
  
We created animation video we created to simply illustrate how we can implement kNN algorithm to classify Diabetic Patient given age and BMI =)
<p align="center" width="100%"><img width="680" alt="Screen Shot 2022-12-06 at 5 04 40 PM" src="https://user-images.githubusercontent.com/97704603/206062418-ad414215-c374-4811-b945-fa29100c191f.png"><p>


[Click me to watch videos👉👈](https://youtu.be/5nogFDZDz_k)

<p align="center">
<img width="660" alt="1" src="https://user-images.githubusercontent.com/97704603/206064649-162bd391-fd11-41b2-bc8e-b38c6694241d.png">
<p>
As you may learn in the following sections, for supervised learning algorithm (classification), we need to have a training dataset before we want to classify the new datapoint. Here is a group of people that we will record their BMI and ages for training dataset generation. (SUPER SIMPLE DATASET)

<p align="center">
<img width="660" alt="2" src="https://user-images.githubusercontent.com/97704603/206064653-d18740b9-0895-49f8-805a-831f1e386d53.png">
<p>
Healthy patients will be marked as pink points on the graph, while diabetic patients will be marked as yellow points.  

<p align="center">
<img width="660" alt="3" src="https://user-images.githubusercontent.com/97704603/206064656-3380a833-f5f4-4feb-81af-02e470ae5e18.png">
<p>
After the machine is given the training dataset, it will be given a new data point, which is needed to be classified. Here, the new data point is a middle-age male with BMI in overweight range.
  
<p align="center">
  <img width="660" alt="4" src="https://user-images.githubusercontent.com/97704603/206064659-cb1effe9-f98b-400a-911d-fbac4630969d.png">
<p>
kNN algorithms(k Nearest Neighbors Algorithm) can be implemented to classify this new data point. k is a user-defined number of neighbors.
We will talk about how to choose k and what kNN algotithm is in our following section.

<p align="center"> 
  <img width="660" alt="6" src="https://user-images.githubusercontent.com/97704603/206064660-1f62aa34-0001-4662-a23d-0d5aaf45690e.png">
<p>
After choosing the k and check the number of neighbors in different groups, this new data point can be classified to diabetes group as it has more yellow point neighbors.

  <br>
  
---
  
# Clustering v.s. Classification <a name="3"></a >
[BACK TO TABLE OF CONTENTS](#tob)

Classification and Clustering are two common machine learning methods to categorize objects into different classes based on features. Classification deals with identifying which new categories does this new object belongs to, on the basis of known labels in a training set of data. 

<br>

For instance, suppose we want to predict whether a student will get an A in BENG183 based on its first 3 homework grades (features). This is a binary classification problem since the outcomes will be:

1. Student gets an A, a result labeled “True”
2. Student does not get an A, a result labeled “False”.

In summary, classification requires a set of observations (training data) which comprises actual classification results (labels). We train the model, called Classifier on this dataset, and use that model to predict whether a student will get an A in BENG183 or not. 

<br>

![Image](https://media.geeksforgeeks.org/wp-content/uploads/classification-1.png)
###### From https://www.geeksforgeeks.org/getting-started-with-classification/
<br>

Clustering deals with dividing the population into subpopulations such that data points in the same groups are more similar within data points in the same group and different between data points in other groups. Clustering does not require any label in the training set so it’s also an unsupervised learning method.


<br>

<p align="center">
<img width="680" alt="2" src="https://media.geeksforgeeks.org/wp-content/uploads/clusteringg.jpg">
<p>
  
###### From https://www.geeksforgeeks.org/clustering-in-machine-learning/

<br>

For instance, if we want to discover whether a newly discovered specie falls into category A or category B, clustering would be a great method to use.

<br>

<p align="center">
<img width="680" alt="2" src="https://upload.wikimedia.org/wikipedia/commons/thumb/7/70/Phylogenetic_tree.svg/900px-Phylogenetic_tree.svg.png">
<p>
  
###### From https://en.wikipedia.org/wiki/Phylogenetic_tree

<br>

More difference between classification and clustering can be found in this table:

|Classification| Clustering |
|:----------------:|:----------------:|
|Uses labelled data as input    |Uses unlabelled data as input|
|Training and testing sets needed| Training and testing sets not needed|
|Supervised learning| Unsupervised learning|
|More complex| Less complex|
|Examples algorithms: Logistic regression, Naive Bayes classifier, Support vector machines, etc.|Examples algorithms: k-means clustering algorithm, Fuzzy c-means clustering algorithm, Gaussian (EM) clustering algorithm, etc.|

  <br>
  
---


# Machine learning - K-nearest-neighbors classification (KNN) <a name="4"></a >
[BACK TO TABLE OF CONTENTS](#tob)
  
KNN is a simple yet effective machine learning classification approaches. This section will explain the details behind K neariest neighbors algorithm.

## Intuition <a name="4.1"></a >
[BACK TO TABLE OF CONTENTS](#tob)
  
> You are who you surround yourself with.
> -- <cite>Jennifer Fedinec</cite>
> 
This is the idea behind KNN algorithm. In the N-dimentional database, given a new datapoints, the KNN will looks at its neighbor to determine its classification. For example, if the majority of its neighbors belongs to class A, the new datapoint will be classified as class A.

To define the size of neighbor, a parameter K will be set beforehand. A larger K will considers more neighbor, while a smaller K will consider less / closer neighbors.

## Implementation <a name="4.2"></a >
[BACK TO TABLE OF CONTENTS](#tob)
  
To dive deep into its implementation, let's consider a case where a unknown sample need to be classified in a 2-D plane.

<p align="center">
<img src="img/Screen%20Shot%202022-12-05%20at%205.46.23%20PM.png" width="500">
<p>

###### From https://www.ibm.com/topics/knn

Here, we see neighbors of both classes surrounding the new example. Let's first define the K for the algorithm to start working.

1. Take in user input to define the parameter k to be 3.

Next, the model will look at the 3 nearest neighbor.

2. The model checks out the 3 neighbors, and get 1 class A and 2 class B data points.

<p align="center">
<img src="img/Screen Shot 2022-12-05 at 5.59.17 PM.png" width="500">
<p>
  
After getting these data, the model will classify the new datapoint to be the majory class of its neighbors.

3. Because there are more class B than class A neighbors, the new datapoints is classified as class B.


## Distance metrics <a name="4.3"></a >
[BACK TO TABLE OF CONTENTS](#tob)
  
On a higher dimentional space which is common in bioinformatic application, difference distance metrics will lead to different results and have their own advantages as well as disadvantages. Let's discuss the two most common distance measurments.

* Euclidean Distance

  The Euclidean distance measure distance in Euclidean space based on Pythagoras' theorem. It is calculated by taking the square root of the sum of the squared pair-wise distances on all dimensions.
  
  <p align="center">
  <img src="img/Screen Shot 2022-12-05 at 6.15.55 PM.png" width="300">
  <p>
    

* Manhattan distances
  
  Instead of calculating the shortest direct path between two points, Manhattan distance calculates the distance based on gridlines.

  <p align="center">
  <img src="img/Screen Shot 2022-12-05 at 6.16.02 PM.png" width="300">
  <p>
    


Both metrics are intuitive and fast to compute, therefore widely used in KNN applications.


## Normalization <a name="4.4"></a >
[BACK TO TABLE OF CONTENTS](#tob)
    
Because large values in some dimentions will overpower and skew the algorithm to ignore dimentions of smaller values, which may inclose important informations, we need a way to standardize all datapoints across all dimentions. This is where normalization comes in.

One simple normalization stratigy is to rescale all features within range 0-1.

## Importance of K <a name="4.5"></a >
[BACK TO TABLE OF CONTENTS](#tob)
    
The only and most curcial hyperparameter to tune for KNN is k.

<p align="center">
<img src="img/Screen Shot 2022-12-05 at 6.27.31 PM.png" width="1000">
<p>
  
A small k will overfit and model and create inaccurate bondaries. A large k will under fit the model and create overly-generalized bondaries. So a common stragies is to try multiple iteration of k and choose the best performing one. This is possible because of the low computational cost of KNN.

  <br>
  
---


  
# Summary <a name="5"></a >
[BACK TO TABLE OF CONTENTS](#tob)


Machine learning algorithms in bioinformatics can be used for prediction, classification, and feature selection. Machine learning has many applications such as in biology and bioinformatics. For instance, Artificial neural networks in bioinformatics have been used for:

* Comparing and aligning RNA, protein, and DNA sequences.
* Identification of promoters and finding genes from sequences related to DNA.
* Interpreting the expression-gene and micro-array data.
* Identifying the network (regulatory) of genes.
* Learning evolutionary relationships by constructing phylogenetic trees.

Prior to the rise of machine learning, bioinformatics calculations had to be done by hand, and this bring difficulty for issues such as protein structure forecasting. Machine learning has already greatly benefited the study of bioinformatics. In the future, we believe that with the advancement of machine learning, bioinformatics will be able to solve more complex biological and public health related problems.




  

