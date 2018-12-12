+++
# Date this page was created.
date = "2018-04-30"

# Project title.
title = "DC-GAN and Style Transfer"

# Project summary to display on homepage.
summary = "EECS 504 Course Project: An implementation of DCGAN and Style Transfer. Then some follow up work is presented: Applied DCGAN to Style Transfer"

# Optional image to display on homepage (relative to `static/img/` folder).
image_preview = "tower_set.jpg"

# Tags: can be used for filtering projects.
# Example: `tags = ["machine-learning", "deep-learning"]`
tags = ["CovNets"]

# Optional external URL for project (replaces project detail page).
external_link = ""

# Does the project detail page use math formatting?
math = true

# Optional featured image (relative to `static/img/` folder).
[header]
image = "sunflower_model1.jpg"
caption = "Fake Sunflower"

+++

## Group Work

**Author:** Tian Pang, Zeyu Sun, Haowei Xiang

Basically, we implement a Deep Convolutional Generative Adverisial Network(DCGAN) to generate fake images (e.g., sunflower and cars in our case). The roughly tuned CNN did well in the sunflower case while did quite poor in the cars case. And we investigate how to use different kind of Style Transfer in terms of their cost function.

### Style Transfer

#### Theory

Style Transfer is a transformation of image that transfer the artistic style of content image to style image. A famous style image is starry night painted by Vincent van Gogh. 

Technically, style transfer is a process to minimize the cost function, which comprises content loss, style loss, total-variance loss. 

Content loss measures the difference of feature map between generated image and original image. First consider a single layer $\ell$, that has feature maps $A^\ell \in \mathbb{R}^{1 \times C_\ell \times H_\ell \times W_\ell}$. $C_\ell$ is the number of filters/channels in layer $\ell$, $H_\ell$ and $W_\ell$ are the height and width. Let $F^\ell \in \mathbb{R}^{N_\ell \times M_\ell}$ be the feature map for the current image and $P^\ell \in \mathbb{R}^{N_\ell \times M_\ell}$ be the feature map for the content source image where $M_\ell=H_\ell\times W_\ell$ is the number of elements in each feature map. Finally, let $w_c$ be the weight of the content loss term in the loss function.$L_c = w_c \times \sum_{i,j} (F_{ij}^{\ell} - P_{ij}^{\ell})^2.$

As for style loss First, compute the Gram matrix G which represents the correlations between the responses of each filter,which is an approximation to the covariance matrix.$G_{ij}^\ell  = \sum_k F^{\ell}_{ik} F^{\ell}_{jk}.$
Assuming $G^\ell$ is the Gram matrix from the feature map of the current image, $A^\ell$ is the Gram Matrix from the feature map of the source style image, and $w_\ell$ a scalar weight term, then the style loss is$L_s^\ell = w_\ell \sum_{i, j} \left(G^\ell_{ij} - A^\ell_{ij}\right)^2,$
Add the style loss for all layers:$L_s = \sum_{\ell \in \mathcal{L}} L_s^\ell.$

Total-variation can be expressed by the difference of every to adjacent pixels, both vertically and horizontally. The loss of three channel of the image(RGB) is added together, and the total summed loss is weighted by the total variation weight, $w_t$:
$L_{tv} = w_t \times \sum_{c=1}^3\sum_{i=1}^{H-1} \sum_{j=1}^{W-1} \left( (x_{i,j+1, c} - x_{i,j,c})^2 + (x_{i+1, j,c} - x_{i,j,c})^2  \right)$.

#### Results

![Tower Set](tower_set.jpg)

### DC-GAN

#### Theory

As mentioned, DCGAN is consist of a generator and a discriminator. The discriminator, which takes an image as input and gives the probability that the input image is a true image, is a convolutional neural network. It convolves 64 * 64 *3 images several times with certain window sizes, strides and depth and give the probability with sigmoid as the output activation function.\\
On the contrary, the generator, which takes random noise as input and generate fake images as output, is a transpose convolutional neural network. It takes 100 random numbers with normal distribution, fully connect them to 4 * 4 * 1024 neurons, reshapes the neurons to 4 * 4 images with 1024 depth, deconvolves them several times and finally generate 64 * 64 * 3 images.

#### Results



## Individual Follow up Work

