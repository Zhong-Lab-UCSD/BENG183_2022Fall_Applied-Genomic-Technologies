# BENG-183: K-means Clustering

**What Is K-Means Clustering?**

K-means clustering is an unsuperivised machine learning algorithm used to cluster data. K-means clustering groups datapoints into k# of clusters centered around centroids (the center of each cluster). 

> **Machine Learning Overview**
> 
> Machine Learning is a type of AI that causes software to self-improve and more accurately predict outcomes without being programmed to do so externally.
> 
> Supervised vs. Unsupervised Learning
> * Supervised learning involves the implementation of a labeled dataset and a test dataset. The labeled dataset is pre-labeled bye the user in order to ‘teach’ the algorithm how to deal with the test dataset.
> * Unsupervised learning involves the implementation of machine learning algorithms to analyze and cluster datasets. Unsupervised learning algorithms complete this without the need for pre-labeling, and are therefore unsupervised.

**Selecting a K value**

There are many different approaches used for selecting k. 

* One simple way is to set k as $\sqrt \frac{n}{2}$, where n is the size of the data set. 

* The elbow method is a conventional way of determining the number of clusters. As shown in the figure below[1], it finds the point where the clustering score becomes stabilized. The corresponding x-corrdinate value gives us the optimal cluster number. There are cases where the “elbow” shape is not obvious (on the right), or the algorithm does not give a proper curve.

<p align="center">
<img src="https://user-images.githubusercontent.com/59674595/206001503-9a307831-5c4c-4587-bd73-0d82d50846ec.png" width="500">
</p>

* An even better method is to calculate the Silhouette coefficient, or the Silhouette width, $s$. It is defined as $s = {(b-a) \over max(a,b)}$, where $a$ stands for the average intra-cluster distance and $b$ stands for the average nearest-cluster distance. If all Silhouette values of data points from a cluster are close to 1, the cluster is well identified. Otherwise, a Silhouette width near -1 indicates that the data point may not belong to this specific cluster[2]. By calculating the average Silhouette width with different choices of k, we can find out the optimal cluster number with the highest $s$. 

* Some other approaches include cross-validation, which splits the data into two or more parts, with one part used for clustering and other parts for validation. Based on the concept of cluster stability, a stable clustering algorithm should produce similar results with data originating from the same source. 

* The information criterion approach is a model selection technique that can also be used to determine number of clusters. It makes decisions among models with different number of parameters while considering both the fit of models and their complexity. 

***

**Algorithm**

We iterate over the algorithm until we reach our desired results or convergence occurs.
Convergence is where the results of the algorithm no longer change. Aka. once centroid and cluster re-assignment no longer changes. 
Convergence
Determines when iteration ceases. Convergence occurs when there is no longer any change in cluster assignment and centroid location. 


<details>
<summary>Visualizing the Algorithm</summary>
<br>
 
<p align="center">
<img width="700" alt="Screen Shot 2022-12-06 at 11 57 55" src="https://user-images.githubusercontent.com/59674595/206010456-5e9b5402-299e-4818-bee3-e9903d553019.png">
</p>
 
<p align="center">
<img width="700" alt="Screen Shot 2022-12-06 at 11 58 04" src="https://user-images.githubusercontent.com/59674595/206010467-26fd65f0-b77e-484e-9602-49e3129d9e37.png">
</p>
<p align="center">
<img width="700" alt="Screen Shot 2022-12-06 at 11 59 08" src="https://user-images.githubusercontent.com/59674595/206010476-6da33c65-1e12-47e2-a50d-f13959ecde3c.png">
</p>
</details>



**Improving the Algorithm**

A heavy focus of improving the algorithm is on the initialization of centroids. Apart from randomly select the initial centroids, other techniques are adopted by scientists as well. One of these include generating random partitions, that is, all the points are put into random clusters and the centroids are calculated afterwards. This works especially well when the clusters highly overlap, but in other cases randomization still has its advantages. 

One another way is the furthest point heuristic, also known as Maxmin. An arbitrary point is picked as the first centroid, then for each of the following centroids, the point that is furthest from its nearest existing centroid is selected. 

When initialization is random, repeating k-means can also significantly increase the accuracy of the clustering result. And if the clusters are separated, initialization dominates the performance of the algorithm. 

***

**Advantages**
 
- Simple algorithm that yields simple results
  * The k-means clustering algorithm is an unsupervised learning algorithm. This means that we do not need to come up with a training set or labels. We can simply select a k-value and get our results.
- Faster time complexity than hierarchical clustering
  * The k-means clustering algorithm uses linear time complexity, which is advantageous over other clustering algorithms such as hierarchical clustering.
- Changes can be easily made to influence clustering
  * Changes can be made to the k-value that significantly impact the clusters that occur. This means that the k-means algorithm allows for more manipulation of the dataset. The algorithm can also stop due to convergence or after a set number of iterations.


**Disadvantages**

- Manual selection of k 
  * The algorithm itself does not guarantee the development of the optimal clustering result, nor does it derive the k value after the algorithm begins. A proper k should be chosen beforehand. 
- Varying result for different runs
  * The initial cluster centers are randomly selected from all the data points of the given input. Thus the clustering can be unstable in different runs. 
- Limited input data
  * The input dataset is required to be numerical, since the notion of distance needs be defined in order to assign data points to their “nearest” centroid. 
- Trouble with messy data
  * K means clustering generates uniform clusters, so it does not function well for unevenly spread data. For data of different density, the clustering would not always be the “best-fit”. The algorithm cannot nicely handle outliers either, and the resulted pattern would be vague. 

***

**Applications**

K-means Clustering is a very useful and applicable algorithm both in biology and other fields. For example, in biology, k-means clustering can be applied to scRNA-seq data to cluster the data into cell types and reveal patterns in the data. Furthermore, k-means clustering can be used in gene co-expression networks to reveal relationships between differnet genes and their expression. Outside of biology, k-means clustering is an algorithm that can be used in marketing to cluster customers, and in geographic analysis can be used to cluster an area into different regions depending on factors such as crime, average household size, etc. 

> **CASE STUDY: Using K-means clustering to identify cell types in scRNA-seq data**
> 
> After performing scRNA sequencing (scRNA-seq), the data can be clustered, using k-means clustering, to reveal different cell types present in the data. The output of scRNA-seq is a FASTQ file storing the raw reads. Prior to performing k-means clustering, the data must first be processed, normalized, and dimensionally reduced. 
><details>
><summary>1. Pre-processing</summary>
><br>
> First, the quality of each read needs to be checked. To check the quality of reads, a tool called FASTQC is used. FASTQC provides a report on the quality of the data, and if the data is deemed good quality the data is now ready to be aligned to the reference genome. There are many tools to perform alignment, one of those is STAR (Spliced Transcripts Alignment to a Reference). The final step of processing involves counting the number of reads that map to each gene. STAR stores the aligned data in a BAM file, there are tools such as featureCounts which take in a BAM file (the alignment output) and output a count matrix (number of reads per gene). See [3] for further details.
></details>
>
><details>
><summary>2. Normalization</summary>
><br>
>The data must be normalized prior to clustering to remove any bias introduced into the data by different factors including, but not limited to, gene length and GC content[4]. One useful tool to normalize scRNA-seq data is scTransform, a function in Seurat. 
></details>
>
><details>
><summary>3. Dimensionality Reduction</summary>
><br>
>Once the data has been normalized, the data must be dimensionaly reduced. This is a necessary step prior to clustering because k-means clustering measures the eucladian distance between data points, and in high-dimensionality space, this is very difficult to measure. One type of dimensionality reduction is PCA (principal component analysis). After performing dimensionality reduction, each cell is represented by a single data point and is mapped to a graphical location. 
></details>
>
><details>
><summary>4. Clustering</summary>
><br>
>At last, the data is ready to be clustered (using k-means clustering)! Clustering results depend on the value of k chosen. K represents the number of clusters. First, each centroid (the center of each cluster) is randomly assigned to the position of a data point. Next, the distance between each centroid and each data point is measured. Then, the data points are assigned to the cluster in which they are closest to (the smallest eucladian distance between a datapoint and a centroid). The algorithm continues until convergence is achieved. See the algorithm section for a more detailed description of how the algorithm works. The final output of the algorithm is the dataset clustered into k # of clusters with each unique data point assigned to a cluster.
></details>

***

**Citations**

1. https://www.researchgate.net/profile/Trupti-Kodinariya/publication/313554124_Review_on_Determining_of_Cluster_in_K-means_Clustering/links/5789fda408ae59aa667931d2/Review-on-Determining-of-Cluster-in-K-means-Clustering.pdf
2. Pasi Franti, Sami Sieranoja. How much can k-means be improved by using better initialization and repeats?, Pattern Recognition, Volume 93, 2019, Pages 95-112, ISSN 0031-3203, https://doi.org/10.1016/j.patcog.2019.04.014.
3. https://hbctraining.github.io/Intro-to-rnaseq-hpc-O2/lessons/05_counting_reads.html
4. https://blog.bioturing.com/2022/01/27/a-guide-to-scrna-seq-normalization/#:~:text=What%20is%20scRNA%2DSeq%20Normalization,level%20of%20biological%20gene%20expression.




