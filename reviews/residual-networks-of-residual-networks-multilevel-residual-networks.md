# Residual Networks of Residual Networks: Multilevel Residual Networks

Ke Zhang, Miao Sun, Tony X. Han, Xingfang Yuan, Liru Guo, Tao Liu, ArXiv, 2016

## Summary

This paper introduces a modification to the ResNets architecture with multi-level shortcut connections (shortcut from input to pre-final layer as level 1, shortcut over each residual block group as level 2, etc) as opposed to single-level shortcut connections in prior work on ResNets. The authors perform experiments with multi-level shortcut connections on regular ResNets, ResNets with pre-activations and Wide ResNets. Combined with drop-path regularization via stochastic depth and exploration over optimal shortcut level number and optimal depth/width ratio to avoid vanishing gradients and overfitting, this architecture achieves state-of-the-art error rates on CIFAR-10 (3.77%), CIFAR-100 (19.73%) and SVHN (1.59%).

## Strengths

- Fairly exhaustive set of experiments over
    - Shortcut level numbers.
    - Identity mapping types: 1) zero-padding shortcuts, 2) 1x1 convolutions for projections and others identity, and 3) all 1x1 convolutions.
    - Residual block size (2 or 3 3x3 convolutional layers).
    - Depths (110, 164, 182, 218) and widths for both ResNets and Pre-ResNets.