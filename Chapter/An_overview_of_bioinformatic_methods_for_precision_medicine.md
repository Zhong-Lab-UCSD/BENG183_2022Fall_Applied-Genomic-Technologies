# An overview of bioinformatic methods for precision medicine

## 1\. Techniques/Methods

Precision Medicine can provide a personalized insight into drug
treatment and disease diagnosis by using machine learning(ML) and
network-based (NB) methods. The issue here, however, is that due to the
vast range of biological factors at play in a person’s physiology, it is
impossible to create such a diagnosis based solely on just one of these
biological markers. The way precision medicine is starting to shift is
to using integrative analysis that utilizes two or more of a person’s
biological markers simultaneously to create a better prediction.

Common methods in machine learning fall under three categories:

![Common Methods in Machine Learning](https://github.com/kelseydang/BENG183_Project/blob/master/BENG183_Project/ML_methods.png)


  - Supervised: methods are commonly used for classification and
    regression and require known labels as input with your data.
    Supervised learning usually involves using a subset of the labeled
    data as a training set and the remaining of the data as the testing
    set to determine its accuracy.  
  - Unsupervised: methods are commonly used for clustering and
    dimensionality reduction and take as input a dataset that is
    unlabeled. For unsupervised learning, hidden patterns can be
    organized into meaningful subsets.  
  - Semisupervised: learning methods takes a mixture of both labeled and
    unlabeled samples that can be used to explain the structure of the
    data as well as make new predictions of unlabeled samples.

Example focused on Supervised Learning:

**Integrating both NB and ML approaches using Proteomics/Interactomics
and Transcriptomics and a support vector machine(SVM) to predict Drug
response**

Affinity-purification Mass Spectrometry(AP-MS) is used to determine the
physical interactions(preys) for a selected protein of interest (Bait)
in a sample; such interactions are known as protein-protein
interaction(PPIs). Selecting a target Bait that we know to be associated
with a specific disease(i.e. cancer) can lead us to other interactors
that could be essential for the development of the cancer phenotype.
After running AP-MS and determining which subset of preys have a strong
interaction, we can look at that subset from publicly available mRNA
expression data from patients who also have data of their response to
cancer treatment drug. Since we are given the drug responses of the
patients (1 for positive response, 0 otherwise), then we can use the
mRNA expression data of \~80% of the patients to train the SVM while
also inputting how those 80% of patients responded to the drug.

![training SVM](https://github.com/kelseydang/BENG183_Project/blob/master/BENG183_Project/TrainingSVM.jpg)

This trains the SVM to try and find a correlation of expression levels
for that subset of preys that had a strong interaction with your
original bait and how that patient responded. We can test the SVM using
the remaining 20% of patient mRNA data into the SVM and comparing how
accurate the predicted response form the SVM is with the actual response
from the given patient data.  

![testing SVM](https://github.com/kelseydang/BENG183_Project/blob/master/BENG183_Project/Testing%20SVM.jpg)

**How a SVM classifies data points: **

#### Linearly separable data:

The SVM is trained with an original set of labeled data and a hyperplane
is created to separate the data and positioned in space so that the
distance between the hyperplane and the closest data points from each
distinct label is maximized. (See figures below) This hyperplane is then
used as a boundary to determine where new data lies and how it is
classified.

![data1](https://github.com/kelseydang/BENG183_Project/blob/master/BENG183_Project/SVM_data1.png)

User input data w/ labels(above)

![data2](https://github.com/kelseydang/BENG183_Project/blob/master/BENG183_Project/SVM_data2.png)

Data points separated by Hyperplane with optimal Maximized Support Vector distances(above)

#### Non-linearly separable data:

Data points aren’t always able to be separated by just a linear line, so in order to account for this the SVM converts the data into a higher dimension where the data is able to be linearly separated by a hyperplane(purple line). Figures below demonstrate how data points can become linearly separable by first being converted to a higher dimension.

![nonlinear](https://github.com/kelseydang/BENG183_Project/blob/master/BENG183_Project/SVM_NonLinear.png)

Demo of SVM:
https://cs.stanford.edu/people/karpathy/svmjs/demo/

Optinoal exercise using R:
http://uc-r.github.io/svm

Example method using Unsupervised Learning:

K-means algorithm is a way of dividing points(genes, samples, cells, etc.) into homogeneous classes or clusters. It analyses data and groups them into a user-defined number of classes(clusters) based on similarity. This method takes in unlabeled data to begin with, the number of clusters desired, and can also take the number of maximum iterations.

#### K-means Algorithm

Start with suitable choices of number of clusters (K). Then:

    1. Assign each points to similar center
    2. Identify the cluster centroid
    3. Reassign the points based on the minimum distance to the new centroid
    4. Identify the new cluster centroids
    5. Repeat steps 3 and 4 until:
    	- Centroids no longer change
	        - Points remain in the same cluster
	        - Or max number of iterations is reached(defined by user)
	
	
![k-means example](https://github.com/kelseydang/BENG183_Project/blob/master/BENG183_Project/kmeans_example_figure.png)

from : https://www.edureka.co/blog/k-means-clustering/




Demo using K-means:
https://stanford.edu/class/ee103/visualizations/kmeans/kmeans.html

Optional exercise:
http://master.bioconductor.org/help/publications/books/bioinformatics-and-computational-biology-solutions/chapter-code/AnalClust.R

#### When to chose SVM or K-Means:

|**SVM**|**K-Means**|
|----|-----------|
|Data has labels, there are a lot of higher dimensions(categories such as genes) in the data|Data labels are unknown, a rough estimate of how many groups are present in data|
|Goal: Further classification of new data into its subtype|Goal: Cluster data to identify similar functions, identify subtypes, or discover shared similarity in DNA|

## 2\. Future Directions

Throughout this chapter we have solely focused on the omics data type of genomics, however there is an ever-growing amount of different omics data types being discovered today that can be incorporated into Precision Medicine. In addition to the abundance of omics data types, there is also a large number of clinical datasets of patient features becoming more available and more complex. In the future, the main focus would be to integrate these datasets and omics to create the most precise treatment for patients. In the figure below, it illustrates only some omics data types, even though there is much more to explore in the future.

![omics](https://github.com/kelseydang/BENG183_Project/blob/master/BENG183_Project/Multi_omics.png)

Some examples of different omics data types are: Transcriptomics, Proteomics and Interactomics, Phenomics and Exposomics. Transcriptomics measures the amount of transcribed genetic material over time. Proteomics and Interactomics focuses on produced proteins, after all translational modification. Phenomics measures the physical and biochemical traits of organisms, while Exposomics encompasses all human environmental, nongenetic, exposures after conception.<sup>23</sup> In the future, PM could not only be more precise and accurate with the growing knowledge of omics data types and the large clinical databases, but it would allow medical practitioners to correctly diagnose a patient and even utilize drug repurposing in giving treatment to patients as well. With the availability of various omics data, computational predictions of new drug candidates for repurposing has necessitated the development of many new methods for data integration, thus patients would be less misdiagnosed and have a greater success rate from the treatment when all of their health information is utilized in selecting treatment.<sup>23</sup>
