# Visualizing and Understanding Convolutional Networks

Matthew D Zeiler, Rob Fergus, ECCV, 2014

## Summary

This paper introduces a novel visualization technique to understand
representations learnt by intermediate layers of a deep convolutional
neural network - DeconvNet. Using DeconvNet visualizations as a
diagnostic tool in different settings, the authors propose changes to the
model proposed by Alex Krizhevsky, which performs slightly better and
generalizes well to other datasets. Key contributions:

- Deconvolutional network
    - Feature activations are mapped back to input pixel space by setting
    other activations in the layer to zero and successively unpooling,
    rectifying and filtering (using the same parameters).
    - Unpooling is approximated by using switch variables to remember
    the location of highest input activation (and hence these visualizations
    are image-specific).
    - Rectification involves passing the signal through a ReLU
    non-linearity.
    - Filtering involves convolving the reconstructed signal with
    the transpose of the convolutional layer filters.
- Well-designed experiments to provide insights

## Strengths

- Observation of evolution of features
    - Visualizations clearly demonstrate that lower layers
    converge within a few epochs and upper layers
    develop after a considerable number of epochs (40-50).
- Feature invariance
    - Visualizations show that small transformations have a
    dramatic effect on lower layers and lesser impact on higher
    layers. The model is fairly stable to translation and scaling,
    not so much to rotation.
- Occlusion sensitivity analysis
    - Parts of the image are occluded, and posterior and activities
    are visualized. Clearly show that activities drop when the object
    is occluded.
- Correspondence analysis
    - The intuition is that CNNs implicitly learn the correspondence between different parts.
    - To verify this, dog images with frontal pose are taken and the same part of the face
    is occluded in each of them. Then the difference in feature maps for each of those and the
    original image is calculated, and the consistency of this difference across all image pairs
    is verified by Hamming distance. Lower scores as compared to random occlusions does show
    that the model learns correspondences.
- Proposed model performs better than Alex Krizhevsky's model, and generalizes
well to other datasets.

## Weaknesses / Notes

- The justification / intuition for choice of smaller filters wasn't convincing
enough.
- Why does removing layer 7 give better top-1 error rate on train and
val?
- Rotation invariance might be something worth looking into.