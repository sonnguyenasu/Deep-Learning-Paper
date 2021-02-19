# Detection Transformer (DETR)

Paper Link: [link](https://arxiv.org/pdf/2005.12872.pdf)

Code Link: [code](https://github.com/facebookresearch/detr)

Interative Colab Notebook: [colab](https://colab.research.google.com/github/facebookresearch/detr/blob/colab/notebooks/detr_demo.ipynb)

Even though Transformer achieved a lot of success recent years in several NLP task, the application of it to Computer Vision is just to be focused. DETR developed by Facebook AI (FAIR) was the very **first** model that apply the Transformer model in Object Detection.

Previously, many (if not all) of object detection algorithms tries to reformulate the problem (to predict different label) or to add prior knowledge (like anchor) in order to solve the problem. 

The ultimate goal of DETR is:
- The first paper that successfully apply transformer in object detection.
- The first competitive end-to-end model that directly output the prediction set without any additional knowledge. 
****
**Problem Formulation**

Given an image **I**, the goal is to find a set of bounding boxes **S** and their according labels. 

DETR output a set of bounding boxes by treating the set as the output of Transformer Decoder. Since the output is a set, we need a loss that is same to all permutation of the output and labels. Also, since output set is not a sequence and all prediction are not time-wise dependence, DETR would output all boxes at once. They achieve these two by 2 methods: Bi-partite Matching Loss for Set Matching and Non-autoregressive Transformer for one-time boxes outputing.

**1. Bi-partite Matching Loss**

**2. Non-autoregressive Transformer**
