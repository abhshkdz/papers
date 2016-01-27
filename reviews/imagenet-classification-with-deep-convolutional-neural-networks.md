# ImageNet Classification with Deep Convolutional Neural Networks

Alex Krizhevsky, Ilya Sutskever, Geoffrey Hinton, NIPS, 2012

## Summary

This paper introduces a deep convolutional neural network (CNN) architecture
that achieved record-breaking performance in the 2012 ImageNet LSVRC. Notably,
it brings together a bunch of neat ideas in an end-to-end, trainable model.
Main contributions:

- Achieves state-of-the-art performance in ILSVRC-2012.
- Makes available an efficient, parallelized GPU implementation of their model.
- Describes in detail the features of their model that help in improving performance
and reducing training time, along with extensive ablative studies.
- Uses data augmentation and dropout to prevent overfitting.

## Strengths

- Uses (and popularizes) ReLUs instead of tanh as the non-linear activation unit, which makes training six times faster.
- Uses local response normalization and overlapped pooling.
- Data augmentation
    - Extracts random crops and performs image translations, horizontal reflections maintaining the label distribution.
    - Alters RGB pixel values by performing PCA on training set, and adding multiples of eigenvalues times a random variable drawn from a Gaussian to image. Provides invariance to changes in intensity and color of illumination.
- Dropout prevents overfitting. Randomly drops half of the neurons in the fully connected layers, and can be interpreted as averaging over exponentially-many dropout networks.

## Weaknesses / Notes

- Lacks theoretical insight. Design decisions are motivated solely by results.