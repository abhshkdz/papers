# Striving for Simplicity: the All Convolutional Net

Jost Tobias Springenberg, Alexey Dosovitskiy, Thomas Brox, Martin Riedmiller, ICLR, 2015

## Summary

This paper simplifies the convolutional network proposed
by Alex Krizhevsky by replacing max-pooling with strided
convolutions (under the assumption that max-pooling is
required only for dimensionality reduction). They also
propose a novel technique for visualizing representations
learnt by intermediate layers that produces nicer visualizations
in input pixel space than DeconvNet (Zeiler et al) and Saliency
map (Simonyan at al) approaches.

## Strengths

- Their model performs at par or better than the original AlexNet formulation.
    - Max-pooling replaced by convolution with stride 2
    - Fully-connected layers replaced by 1x1 convolutions and global averaging + softmax
    - Smaller filter size (same intuition as VGGNet paper)
- Combining the DeconvNet (Zeiler et al.) and backpropagation (Simonyan et al.) approaches
at the ReLU operator (which is the only point of difference) by masking out values where at
least one of input activation or output reconstruction is negative (guided backprop) is neat
and leads to nice visualizations.

## Weaknesses / Notes

- Saliency maps generated from guided backpropagation definitely look much better
as compared to DeconvNet visualizations and saliency maps from Simonyan et al's paper.
It works better probably because the negative saliency values only arise from the very
first convolution, since negative error signals are never propagated back through the
non-linearities.