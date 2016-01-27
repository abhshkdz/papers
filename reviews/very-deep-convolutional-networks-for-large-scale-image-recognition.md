# Very Deep Convolutional Networks for Large-Scale Image Recognition

Karen Simonyan, Andrew Zisserman, ArXiv, 2014

## Summary

This paper proposes a modified convolutional network architecture
by increasing the depth, using smaller filters, data augmentation
and a bunch of engineering tricks, an ensemble of which
achieves second place in the classification task and first place
in the localization task at ILSVRC2014.

Main contributions:

- Experiments with architectures with different depths from 11 to
19 weight layers.
- Changes in architecture
    - Smaller convolution filters
    - 1x1 convolutions: linear transformation of input channels
    followed by a non-linearity, increases discriminative capability
    of decision function.
- Varying image scales
    - During training, the image is rescaled to set the length of the shortest side
    to S and then 224x224 crops are taken.
    - Fixed S; S=256 and S=384
    - Multi-scale; Randomly sampled S from [256,512]
    - This can be interpreted as a kind of data augmentation by scale jittering,
    where a single model is trained to recognize objects over a wide range of scales.
    - Single scale evaluation: At test time, Q=S for fixed S and Q=0.5(S_min + S_max)
    for jittered S.
    - Multi-scale evaluation: At test time, Q={S-32,S,S+32} for fixed S and Q={S_min,
    0.5(S_min + S_max), S_max} for jittered S. Resulting class posteriors are averaged.
    This performs the best.
- Dense v/s multi-crop evaluation
    - In dense evaluation, the fully connected layers are converted to convolutional
    layers at test time, and the uncropped image is passed through the fully convolutional net
    to get dense class scores. Scores are averaged for the uncropped image and its
    flip to obtain the final fixed-width class posteriors.
    - This is compared against taking multiple crops of the test image and averaging scores
    obtained by passing each of these through the CNN.
    - Multi-crop evaluation works slightly better than dense evaluation, but the methods
    are somewhat complementary as averaging scores from both did better than each of them
    individually. The authors hypothesize that this is probably because of the different
    boundary conditions: when applying a ConvNet to a crop, the convolved feature maps are padded with zeros, while in the case of dense evaluation the padding for the same crop naturally comes from the neighbouring parts of an image (due to both the convolutions and spatial pooling), which substantially increases the overall network receptive field, so more context is captured.

## Strengths

- Thoughtful design of network architectures and experiments to study the effect of
depth, LRN, 1x1 convolutions, pre-initialization of weights, image scales,
and dense v/s multi-crop evaluations.


## Weaknesses / Notes

- No analysis of how much time these networks take to train.
- It is interesting how the authors trained a deeper model (D,E)
by initializing initial and final layer parameters with those from
a shallower model (A).
- It would be interesting to visualize and see the representations
learnt by three stacked 3x3 conv layers and one 7x7 conv layer, and
maybe compare their receptive fields.
- They mention that performance saturates with depth while going
from D to E, but there should have been a more formal characterization
of why that happens (deeper is usually better, yes? no?).
- The ensemble consists of just 2 nets, yet performs really well.