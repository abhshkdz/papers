# Deep Inside Convolutional Networks: Visualising Image Classification Models and Saliency Maps

Karen Simonyan, Andrea Vedaldi, Andrew Zisserman, ICLR, 2014

## Summary

This paper attempts to understand the representations learnt by deep
convolutional neural networks by introducing two interpretable visualization
techniques. Main contributions:

- Class model visualizations
    - These are obtained by making numerical optimizations in the input
    space to maximize the class score. Gradients are calculated wrt input
    and are used to update the input image (initialized with zero image),
    while weights are kept fixed to those obtained from training.
- Image-specific saliency map visualizations
    - These are approximated by using the same gradient as before (gradient
    of class score wrt input). The absolute pixel-wise max across channels produces
    the saliency map.
- Relation between DeconvNet and optimization-based visualizations
    - Visualizations using DeconvNet are the same as gradient-based methods except
    for ReLU. In regular backprop, gradients flow through ReLU to units with positive
    input activations, whereas in case of a DeconvNet, it is computed on positive output
    reconstructions.

## Strengths

- The visualization techniques are simple ideas and the results are interpretable. They show
that the method proposed by Erhan et al. in an unsupervised setting is useful to CNNs trained
in a supervised manner as well.
- The image-specific class saliency can be interpreted as those pixels which need to be changed
the least to have a maximum impact on the classification score.
- The relation between DeconvNet visualizations and optimization-based visualizations is
insightful.

## Weaknesses / Notes

- The thinking behind initializing with zero image and L2 regularization in class model
visualizations was missing.