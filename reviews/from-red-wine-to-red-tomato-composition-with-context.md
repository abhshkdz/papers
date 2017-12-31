# From Red Wine to Red Tomato: Composition with Context

Ishan Misra, Abhinav Gupta, Martial Hebert, CVPR, 2017

## Summary

This paper presents a neat approach to compose classifiers for known visual
concepts, in order to recognize complex compositions of these concepts in a
zero/low-shot learning fashion.

- Specifically, they learn linear classifiers for attributes and objects
separately, and then a transformation network to compose them
in model space into (attribute, object) classifiers.

- The transformation network takes SVM parameters of primitive classifiers
(2 or more) and outputs parameters for the joint classifier.
For example, given separate classifiers for small, red, elephant, snake
we can get classifiers for (small, elephant), (red, elephant),
(small, snake), (red, snake) from the transformation network.
