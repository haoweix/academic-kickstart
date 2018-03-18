+++
title = "Comparison of some simple classifiers for MNIST dataset"
date = "2018-03-15"

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = ["Haowei Xiang"]

# Publication type.
# Legend:
# 0 = Uncategorized
# 1 = Conference proceedings
# 2 = Journal
# 3 = Work in progress
# 4 = Technical report
# 5 = Book
# 6 = Book chapter
publication_types = ["0"]

# Publication name and optional abbreviated version.
publication = ""
publication_short = ""

# Abstract and optional shortened version.
abstract = "Principle Component Analysis(PCA), Logistic regression, Neuron Networks(NN), and Support Vector Machine(SVM) will be used here. The goal of this blog is to learn how to design a classifer for MNIST hand-written number dataset"
abstract_short = ""

# Featured image thumbnail (optional)
image_preview = ""

# Is this a selected publication? (true/false)
selected = false

# Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter the filename (excluding '.md') of your project file in `content/project/`.
projects = ["deep-learning"]

# Links (optional).
url_pdf = "http://arxiv.org/pdf/1512.04133v1"
url_preprint = ""
url_code = "https://github.com/haoweix"
url_dataset = ""
url_project = ""
url_slides = ""
url_video = ""
url_poster = ""
url_source = ""

# Does the content use math formatting?
math = true

# Does the content use source code highlighting?
highlight = true

# Featured image
# Place your image in the `static/img/` folder and reference its filename below, e.g. `image = "example.jpg"`.
[header]
image = ""
caption = ""

+++



**The Goal of this post**: is to summarize some interesting supervised machine learning approach, which classfify MNIST hand-writen digit dataset.

**Method**: According to the timeline that I have been exposed, subspace learning, logistic regressions, PCA or so called eigenface, SVM and Neuron Networks will be introduced here.  

**Results**: It's natural to expect that complicated model will have lower test error. Here we will see the accuracy is not proportional to the time of training data.

**Implementation**: Currently these methods are implemented respectively by Julia, MATLAB, and python. I will try to rewrite them all in python if I have time (probably in the summer).

### Subspace Learning

Subspace learning is one simple direct application of singular value decomposition(SVD), which is easy to understand and implement. Such an big disadvantage of this method is that it is especially time-consuming since we need to compute the SVD of a d*n matrix, where $d=28 * 28$ and n is the number of training sample.

### PCA(eigenface)

This is a related method to subspace learning. While subspace learning separately calculate SVD of each class, PCA regard the training data as a hole and find the eigenvectors of scatter matrix coresponding to the largest eigenvalues.

### logistic Regression

Logistic regression is one of the most widely used classify method across the world even for those non-machine learning field. A simple reason for that it is easily to implement and trained, and results is also somehow satisfying.

### SVM

SVM can implemented simply by using python sk-learn library. What need to be tuned are the hyperparameter C and $\gamma$, which can be done by cross-validation, either by sk-learn library or writing one's own.

**Rough result**: training set size and test set size are both 10000. After tuning C=3 and $\gamma$=0.05, the test accuracy is 96.57%, which is much higher than subspace learning and logistic regression.

### Fully connected NN

2 layers and 3 layers NN are used here.

**Dataset**: Training set size is 10000 and test set size is 1000.

**Training method**: Xaxier's method and Mini-batch gradient descent(batch size =500). 

**2 layers NN**: There are 50 neurons in the hidden layer. 

​	Training accuracy is 100% after 500 epochs. Test error is 95.00%.

{{< figure src="/img/pr1accr.jpg" title="2 layer NN accuracy" >}}

{{< figure src="/img/pr1loss.jpg" title="2 layer NN loss" >}}

**3 layers NN**: There 50 neurons in first hidden layer and 30 neurons in the second hidden layer.

​	Training accuracy after 100 epoch is 100%, test accuracy is 95.50%.

{{< figure src="/img/pr2accr.jpg" title="3 layer NN accuracy" >}}

{{< figure src="/img/pr2loss.jpg" title="3 layer NN loss" >}}

### CNN

A simple 2 layers CNN.

| Tables        |      Are      |  Cool |
| :------------ | :-----------: | ----: |
| col 3 is      | right-aligned | $1600 |
| col 2 is      |   centered    |   $12 |
| zebra stripes |   are neat    |    $1 |