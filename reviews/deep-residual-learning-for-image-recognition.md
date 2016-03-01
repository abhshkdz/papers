# Deep Residual Learning for Image Recognition

Kaiming He, Xiangyu Zhang, Shaoqing Ren, Jian Sun, ArXiv, 2016

## Summary

This paper introduces Residual Nets (ResNets), which was the
winning submission (152-layer deep) at ILSVRC 2015 and MS-COCO 2015, and achieves
a top-5 error rate of 3.57% (ensemble of two  nets). Main contributions:

- The key idea is that deeper networks face the degradation problem, i.e.
higher training and test error than shallower nets, because they're harder
to optimize for approximating identity mapping by multiple non-linear layers.
    - They mitigate this problem by forcing solvers to learn residual functions
    i.e. f(x) = H(x) - x, by adding shortcut connections. If identity mapping is
    the optimal formulation, the learned weights should drive f(x) to 0 (and they
    observe that this is a suitable preconditioning as most residual function responses
    are small).

- Shortcut connections (for identity mapping) don't require additional parameters.
    - Size transformations are done by zero-padding (no parameters) or projections. Projections
    introduce additional parameters and perform slightly better.

- Bottleneck design is used to further reduce computational complexity, i.e. 1x1 convolutional
layers before and after 3x3 convolutions to reduce and increase dimensions.

- For detection and localization tasks, they use ResNets in the Faster-RCNN setting.

## Strengths

- ResNets are significantly deeper and more accurate yet computationally cheaper than VGG.

- A single ResNet outperforms previous state-of-the-art ensembles. Their final winning submission
is an ensemble of two networks.

## Weaknesses / Notes

- The idea of shortcut connections to force blocks to learn residual functions preconditioned
on identity mapping is neat, and more so because it doesn't require additional parameters.

- A lot of results and design decisions merit further investigation and reasoning.
    - Why do shortcuts skip 2 or 3 layers? What happens to performance if we increase the number of layers skipped?
    - How well do shortcut connections work with Inception modules? The statistical principles
    underlying both these architectures seem to be orthogonal, does performance further improve?
    - 152 seems to be an arbitrary number of layers that 'worked'.

- The degradation problem seen when making networks deeper by initializing
layers with identity weight matrices seems to be contradictory to the results
presented in the Net2Net paper.