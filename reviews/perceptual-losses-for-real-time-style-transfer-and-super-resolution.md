# Perceptual Losses for Real-Time Style Transfer and Super-Resolution

Justin Johnson, Alexandre Alahi, Li Fei-Fei, ArXiv, 2016

## Summary

This paper proposes the use of pretrained convolutional neural networks that have already learned to encode semantic information as loss functions for training networks for style transfer and super-resolution. The trained networks corresponding to selected style images are capable of performing style transfer for any content image with a single forward pass (as opposed to explicit optimization over output image) achieving as high as 1000x speedup and similar qualitative results as Gatys et al. Key contributions:

- Image transformation network
    - Convolutional neural network with residual blocks and strided & fractionally-strided convolutions for in-network downsampling and upsampling. 
    - Output is the same size as input image, but rather than training the network with a per-pixel loss, it is trained with a feature reconstruction perceptual loss.

- Loss network
    - VGG-16 with frozen weights 
    - Feature reconstruction loss: Euclidean distance between feature representations
    - Style reconstruction loss: Frobenius norm of the difference between Gram matrices, performed over a set of layers.

- Experiments
    - Similar objective values and qualitative results as explicit optimization over image as in Gatys et al for style transfer
    - For single-image super-resolution, feature reconstruction loss reconstructs fine details better and 'looks' better than a per-pixel loss, even though PSNR values indicate otherwise. Respectable results in comparison to SRCNN.

## Weaknesses / Notes

- Although fast, limited by styles at test-time (as opposed to iterative optimizer that is limited by speed and not styles). Ideally, there should be a way to feed in style and content images, and do style transfer with a single forward pass.