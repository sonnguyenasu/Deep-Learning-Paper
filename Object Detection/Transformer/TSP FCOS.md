# TSP-FCOS: Transformer Detector using FCOS Idea

paper link: [link](https://arxiv.org/abs/2011.10881) 

code link: *not published*

*Precaution*: This paper is highly related to DETR and FCOS paper, if you are not familiar with these two, plese consider having a look at the two paper and/or my review at [*fcos*](https://github.com/tson1997/Deep-Learning-Paper/blob/main/Object%20Detection/One-Stage/FCOS.md) and [*detr*](https://github.com/tson1997/Deep-Learning-Paper/blob/main/Object%20Detection/Transformer/DETR.md).

****
## Introduction

As soon as Facebook release their first detection algorithm applying Transformer mechanism, [DETR](https://github.com/tson1997/Deep-Learning-Paper/blob/main/Object%20Detection/Transformer/DETR.md), there are many follow up work trying to optimize their training scheme and the DETR model in general. TSP FCOS (short for Transformer Set Prediction with FCOS) is one of the method that tackling problem with DETR. In short, TSP FCOS applies many tricks inspired from [FCOS](https://github.com/tson1997/Deep-Learning-Paper/blob/main/Object%20Detection/One-Stage/FCOS.md) to tackle DETR's long training time. In my opinion, there are 2 main ideas in TSP FCOS:

- The model uses Transformer Encoder only, instead of using both encoder and decoder like in the original paper.
- The model proposes Feature of Interest Module to optimize data feed into the Transformer Encoder.
****
## Problem Formulation
Given an image I, the goal of TSP FCOS is to directly find the set S of bounding boxes and their corresponding class id. In order to do so, TSP FCOS devide the stage of the problem into two sub-problems: Feature of Interest (FoI) finding, and Set Prediction using bipartite matching.

1. Feature of Interest Finding:
   
   The goal of this step is to find the most informative feature vectors in the whole feature map. The model chooses top k vectors that has highest center score. The loss and optimization of this is similar to FCOS.
   
2. Bipartite matching:

    The goal of this step is to predict set ***S*** of bounding boxes from the k input vectors. The format of the output will contain bounding box information ***(cx, cy, w, h)*** and their corresponding class id ***c_i***.

****
## Proposed Solution

**1. Feature of Interest**
   
In this step, the model applys the whole method of FCOS, where they define center+classification branch alongwith bounding box regression branch. After getting the center mask, the model simply chooses the top-k highest score on the center mask and choose them as the Feature of Interest to feed into Transformer Encoder.

**2. Set Prediction**
    
The top-k feature vectors from the previous step are then combined with Positional Encoding and then feed into Transformer Encoder. The encoder was then output a set of predictions, this set will contain information of the bounding boxes: coordinate of the center and class number.

**3. Positional Encoding**

For a feature point with normalized position (x,y) (0<= x,y<=1), its positional encoding is defined as [PE(x):PE(y)] (: denotes concatenate), with:

$$PE(x)_{2i} = sin(x/10000^{2i/d_{model}})$$
$$PE(x)_{2i+1} = cos(x/10000^{2i/d_{model}})$$

here $d_{model}$ is the final depth of the output of previous step.

**4. Transformer Encoder**

*Input*: 

Output of FCOS stage is a tensor of size (CxHxW). If the implementation is similar to DETR, this tensor was then pass through a 1x1 convolution to reduce the depth to d. In Feature of Interest step, we extract only top k center score, so we get a tensor of shape (Cxk) (or dxk).

This d x k mask was then added with the positional encoding, and pass to Transformer Encoder. Notice that the positional encoding is being done at every multihead attention layer since output of such layer are permutation invariant (i.e. they are the same for every permutation of the k vectors)

*Output*:

**5.Faster set prediction training**

For the set of prediction, a feature point can be assigned to ground-truth object only when the point is in the bounding box of the object and in proper pyramid level, i.e. the center must be in some boxes.

Then, we determine the optimal permutation of the prediction set by a process similar to DETR, and optimize the Hungarian loss on such permutation and the ground truth to optimize the final set result.
