# Object Detection

Object detection is one of the core problems in Computer Vision. The goal of object detection is to locate and label all the objects within a single image.

Among the family of object detector, we have 2 ways to predict our result. One way is by first predicting important regions first and then refining and classifying the resulted region of interest. The other way is directly predict the bounding boxes.

Another way of classifying object detection algorithms is to look at the methods they are using: whether they use anchors or not. If there is involvement of anchor, the method is anchor-based, else we would call it anchor-free.

There are some difficulties of object detection problem that are addressed by all the paper:
- The number of objects in an image varies and we do not know in advance how many there are.
- The object's shape may vary.
- There can be objects that are overlap or occluded.
<details>
<summary style='font-size:20px;'>Two-stage methods</summary>

- [Faster RCNN](https://github.com/tson1997/Deep-Learning-Paper/blob/main/Object%20Detection/Two-Stage/Faster%20RCNN.md)
  
</details>

<details>
<summary style='font-size:20px;'>One-stage methods</summary>

- [Fully Convolutional One Stage Detector (FCOS)](https://github.com/tson1997/Deep-Learning-Paper/blob/main/Object%20Detection/One-Stage/FCOS.md)

- [CenterNet: Object as Points](https://github.com/tson1997/Deep-Learning-Paper/blob/main/Object%20Detection/One-Stage/CenterNet.md) 
-
</details>

<details>
<summary style='font-size:20px;'>Transformer methods</summary>

- [Detection Transformer (DETR)](https://github.com/tson1997/Deep-Learning-Paper/blob/main/Object%20Detection/Transformer/DETR.md)

</details>

