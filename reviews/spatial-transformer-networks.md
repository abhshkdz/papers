# Spatial Transformer Networks

Max Jaderberg, Karen Simonyan, Andrew Zisserman, Koray Kavukcuoglu, NIPS, 2015

## Summary

This paper introduces a neural networks module that can learn input-dependent
spatial transformations and can be inserted into any neural network. It supports
transformations like scaling, cropping, rotations, and non-rigid deformations.
Main contributions:

- The spatial transformer network consists of the following:
    - Localization network that regresses to the transformation parameters
    given the input.
    - Grid generator that uses the transformation parameters to produce a
    grid to sample from the input.
    - Sampler that produces the output feature map sampled from the input
    at the grid points.

- Differentiable sampling mechanism
    - The sampling is written in a way such that sub-gradients can be defined
    with respect to grid coordinates.
    - This enables gradients to be propagated through the grid generator and
    localization network, and for the network to jointly learn the spatial
    transformer along with rest of the network.

- A network can have multiple STNs
    - at different points in the network, to model incremental transformations
    at different levels of abstraction.
    - in parallel, to learn to focus on different regions of interest. For example,
    on the bird classification task, they show that one STN learns to be a head detector,
    while the other focuses on the central part of the body.

## Strengths

- Their attention (and by extension transformation) mechanism is differentiable
as opposed to earlier works on non-differentiable attention mechanisms that used
reinforcement learning (REINFORCE). It also supports a richer variety of
transformations as opposed to earlier works on learning transformations, like DRAW.

- State-of-the-art classification performance on distorted MNIST, SVHN, CUB-200-2011.

## Weaknesses / Notes

This is a really nice way to generalize spatial transformations in a differentiable
manner so the model can be trained end-to-end. Classification performance, and more
importantly, qualitative results of the kind of transformations learnt on larger datasets
(like ImageNet) should be evaluated.