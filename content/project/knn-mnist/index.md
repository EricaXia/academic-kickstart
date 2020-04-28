---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Classification of MNIST Handwritten Digits using K-Nearest-Neighbors in R"
summary: ""
authors: []
tags: []
categories: []
date: 2018-12-31T11:02:38-08:00

# Optional external URL for project (replaces project detail page).
external_link: ""

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Custom links (optional).
#   Uncomment and edit lines below to show custom links.
# links:
# - name: Follow
#   url: https://twitter.com
#   icon_pack: fab
#   icon: twitter

url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: ""
---
### Supervised machine learning classification
#### Data: Handwritten numerical digits pulled from MNIST (Modified National Institute of Standards and Technology database)

### Model: K-Nearest Neighbors Classifier

<br />

## How the KNN Function Works
Using the class labels of the "k" closest neighboring observations from the train set, the KNN algortihm classifies a given observation. The power of the algorithm will depend on the power of "k" and which distance metric is used. Distance metrics include Euclidan, Manhattan, or Minkowski measures of distance.



<br />



## 10-fold Cross Validation to Estimate the Error Rate for KNN

In order to make cross validation run efficiently, I first calculated the distance matricies (for Euclidean and Manhattan distance metrics) beforehand, then ordered the matricies from least to greatest and obtained the index labels. The data was shuffled randomly and split into ten folds by assigning each observation a number from 1 to 10. The folds were stored in a list of indicies. My cv_error_knn function applies the same process to each of the ten folds: the distance matrix is subsetted using the current fold, before being passed to the knn function. My knn function had to be altered slightly so it would accept a distance matrix as a parameter, rather than a distance metric. Each iteration of the loop resulted in a vector of predictions which is compared to the real values to estimate an error rate. Finally, I took the average of the ten error rates to get my overall error rate. For k = 3 neighbors, my estimated cross validation error is about 0.01495, or 1.5%. (The error will differ slightly each time the function is run, but it stays around the same range.)

<br />


## Graphically Displaying the Average Digit

![](https://github.com/EricaXia/knn_digits/raw/main_code/images/mnist_var_img.png)