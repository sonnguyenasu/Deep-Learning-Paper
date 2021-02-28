# Capsule Network: Dynamic Routing between Capsules

paper link: [paper](https://arxiv.org/pdf/1710.09829.pdf)

code link: [code](https://github.com/gram-ai/capsule-networks)

## Introduction

Even though Deep Learning gained the popularity in the family of representation learing and had shown a lot of its power on many kinds of data, there has been some critics on the existence of it. The strongest argument against Deep Neural Network is their ability to interpret is fairly low and their performance can be sub-optimal. People have tried several ways to visualize deep network, or make it more robust. This paper presents the idea of Capsule Net with dynamic routing as an alternative deep learning method beside deep convolutional network for image data, with the obvious strength of being easier to explain and visualize.

****
## Capsule Network

**1. Capsule**
   
A capsule is a group of neurons. Its output, instead of being a single scalar like a neuron, is a vector called "*activation vector*". This activation vector serves 2 roles:
- whether the object entity (object or object's part) is in the image
- what kind of properties does the object entity has

The presence of object entity is represented by the activation vector's length (being normalized so that we can have a probability), while the properties are represented by activation vector's orientation.

**2. Capsule network**

A capsule networks consists of multiple layers of capsules. The current layer refers to the previous layer as its parent and to the next layer as its children. The name is like that because the structure of a capsule network is like a parse tree, where connection between node (or capsule) was dynamically determined.