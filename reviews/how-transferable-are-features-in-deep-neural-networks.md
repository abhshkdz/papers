# How transferable are features in deep neural networks?

Jason Yosinski, Jeff Clune, Yoshua Bengio, Hod Lipson, NIPS, 2014

## Summary

This paper studies the transferability of features learnt at different layers
of a convolutional neural network. Typically, initial layers of a CNN learn
features that resemble Gabor filter or color blobs, and are fairly general, while
the later layers are more task-specific. Main contributions:

- They create two splits of the ImageNet dataset (A/B) and explore how performance
varies for various network design choices such as
    - Base: CNN trained on A or B.
    - Selffer: first n layers are copied from a base network, and the rest of the
    network is randomly initialized and trained on the same task.
    - Transfer: first n layers are copied from a base network, and the rest of the
    network is trained on a different task.
    - Each of these 'copied' layers can either be fine-tuned or kept frozen.

- Selffer networks without fine-tuning don't perform well when the split is somewhere
in the middle of the network (n = 3-6). This is because neurons in these layers co-adapt
to each other's activations in complex ways, which get broken up when split.
    - As we approach final layers, there is lesser for the network to learn and so these
    layers can be trained independently.
    - Fine-tuning a selffer network gives it the chance to re-learn co-adaptations.

- Transfer networks transferred at lower n perform better than larger n, indicating
that features get more task-specific as we move to higher layers.
    - Fine-tuning transfer networks, however, results in better performance. They argue
    that better generalization is due to the effect of having seen the base dataset,
    even after considerable fine-tuning.

- Fine-tuning works much better than using random features.

- Features are more transferable across related tasks than unrelated tasks.
    - They study transferability by taking two random data splits, and splits of
    man-made v/s natural data.

## Strengths

- Experiments are thorough, and the results are intuitive and insightful.

## Weaknesses / Notes

- This paper only analyzes transferability across different splits of ImageNet
(as similar/dissimilar tasks). They should have reported results on transferability
from one task to another (classification/detection) or from one dataset to another
(ImageNet/MSCOCO).

- It would be interesting to study the role of dropout in preventing co-adaptations
while transferring features.