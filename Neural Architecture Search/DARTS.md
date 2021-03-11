# DARTS: Differentiable Architecture Search

Paper link: [paper](https://arxiv.org/pdf/1806.09055.pdf) 

Code link: [code](https://github.com/quark0/darts) 

****
## Introduction
This paper is the first paper that address the issue of discrete search in NAS algorithms. In other words, since NAS algorithms often treat the problems of architecture search as finding computational graphs with discrete set of operations, they are not differentiable, and not capable of gradient optimization methods. There are some works on continuous search space, but they have constraint on hyper-parameters and available search options. DARTS, combining the strength of both world, helps searching Architecture of the network much faster and efficient while keeping the search space flexibility it needs to not decrease performance.
****
## Problem Formulation
Given a supervised dataset (train/test/val), we will try to design a block of nodes called cell, and stack the cell together to achieve optimal performance on the validation dataset given trained ones. The minor goal of this paper is to make such cell architecture finding process differentiable so that we can use gradient descent on it.
****
## Proposed Methods
1. Search space:
   
   It includes a set of operations that we are going to choose which one should be the connection between nodes. The space is limited to a cell instead of global search space. That is to say, DARTS will look for optimal cell that performs well on validation set and stack the cells together to form the network.
2. Search strategy
   
   Let O be a set of candidate operations (e.g. convolution, max pooling, zero) where each operation represents some function. the connection between 2 node i and j is represent by the function <img src="https://render.githubusercontent.com/render/math?math=\hat{o}^{(i,j)}(x)"> given by the formula:

   <img src="https://render.githubusercontent.com/render/math?math=\hat{o}^{(i,j)}(x) = \sum_{o \in O} \frac{\exp(\alpha_o^{(i,j)})}{\sum_{o'\in O}\exp(\alpha_{o'}^{(i,j)})} o(x)">

   where the operation mixing weights for a pair of nodes.

   The strategy is to find:

   <img src="https://render.githubusercontent.com/render/math?math=\min_{\alpha} L_{val}(w^*(\alpha),\alpha)">
   such that <img src="https://render.githubusercontent.com/render/math?math=w^*(\alpha)=\argmin_w L_{train}(w,\alpha)">