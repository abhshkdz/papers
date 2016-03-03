# DenseCap: Fully Convolutional Localization Networks for Dense Captioning

Justin Johnson, Andrej Karpathy, Li Fei-Fei, ArXiv, 2015

## Summary

This paper introduces the task of dense captioning and proposes
a network architecture that processes an image and produce region descriptions
in a single pass and can be trained end-to-end. Main contributions:

- Dense captioning
    - Generalization of object detection (caption consists of single word)
    and image captioning (region consists of whole image).

- Fully convolution localization network
    - Fully differentiable, can be trained jointly with the rest of the network
    - Consists of a region proposal network, box regression (similar to Faster R-CNN)
    and bilinear interpolation (similar to Spatial Transformer Networks) for
    sampling.

- Network details
    - Convolutional layer features are extracted for image
    - For each element in the feature map, k anchor boxes of different aspect ratios
    are selected in the input image space.
    - For each of these, the localization layer predicts offsets and confidence.
    - The region proposals are projected on the convolutional feature map and a sampling
    grid is computed from output feature map to input (bilinear sampling).
    - The computed feature map is passed through an MLP to compute representations
    corresponding to each region.
    - These are passed (in a batch) as the first word to an LSTM (Show and Tell) which
    is trained to predict each word of the caption.

## Strengths

- Fully differentiable 'spatial attention' mechanism (bilinear interpolation)
in place of RoI pooling as in the case of Faster R-CNN.
    - RoI pooling is not differentiable with respect to the input proposal coordinates.

- Fast, and impressive qualitative results.

## Weaknesses / Notes

The model is very well engineered together from different works (Faster R-CNN +
Spatial Transformer Networks + Show & Tell).