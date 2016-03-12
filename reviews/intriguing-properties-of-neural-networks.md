# Intriguing Properties of Neural Networks

Christian Szegedy, Wojciech Zaremba, Ilya Sutskever, Joan Bruna, Dumitru Erhan, Ian Goodfellow, Rob Fergus, ICLR, 2014

## Summary

The paper introduces two key properties of deep neural networks:

- Semantic meaning of individual units.
    - Earlier works analyzed learnt semantics by finding images that maximally activate individual units.
    - Authors observe that there is no difference between individual units and random linear combinations of units.
    - It is the entire space of activations that contains the bulk of semantic information.

- Stability of neural networks to small perturbations in input space.
    - Networks that generalize well are expected to be robust to small perturbations in the input, i.e. imperceptible noise in the input shouldn't change the predicted class.
    - Authors find that networks can be made to misclassify an image by applying a certain imperceptible perturbation, which is found by maximizing the network's prediction error.
    - These 'adversarial examples' generalize well to different architectures trained on different data subsets.

## Strengths

- The authors propose a way to make networks more robust to small perturbations by training them with adversarial examples in an adaptive manner, i.e. keep changing the pool of adversarial examples during training. In this regard, they draw a connection with hard-negative mining, and a network trained with adversarial examples performs better than others.

- Formal description of how to generate adversarial examples and mathematical analysis of a network's stability to perturbations are useful studies.

## Weaknesses / Notes

- Two images that are visually indistinguishable to humans but classified differently by the network is indeed an intriguing observation.

- The paper feels a little half-baked in parts, and some ideas could've been presented more clearly.
