# Delving Deeper into Convolutional Networks for Learning Video Representations

Nicolas Ballas, Li Yao, Chris Pal, Aaron Courville, ICLR, 2016

## Summary

This paper presents a neat method for learning spatio-temporal representations from videos. Convolutional features from intermediate layers of a CNN are extracted, to preserve spatial resolution, and fed into a modified GRU that can (in theory) learn infinite temporal dependencies. Main contributions:

- Their variant of GRU (called GRU-RCN) uses convolution operations instead of fully-connected units.
    - This exploits the local correlation in image frames across spatial locations.
    - Features from pool2, pool3, pool4, pool5 are extracted and fed into independent GRU-RCNs. Hidden states at last time step are now feature volumes, which are average pooled to reduce to 1x1 spatially, and fed into a linear + softmax classifier. Outputs from each of these classifiers is averaged to get the final prediction.

- Other variants that they experiment with are bidirectional GRU-RCNs and stacked GRU-RCNs i.e. GRU-RCNs with connections between them (with maxpool operations for dimensionality reduction).
    - Bidirectional GRU-RCNs perform the best.
    - Stacked GRU-RCNs perform worse than the other variants, probably because of limited data.

- They evaluate their method on action recognition and video captioning, and show significant improvements on a CNN+RNN baseline, comparing favorably with other state-of-the-art methods (like C3D).

## Strengths

- The idea is simple and elegant. Earlier methods for learning video representations typically used 3D convolutions (k x k x T filters), which suffered from finite temporal capacity, or RNNs sitting on top of last-layer CNN features, which is unable to capture finer spatial resolution. In theory, this formulation solves both.

- Changing fully-connected operations to convolutions has the additional advantage of requiring lesser parameters (n\_input x n\_output x input\_width x input\_height v/s n\_input x n\_output x k\_width x k\_height).