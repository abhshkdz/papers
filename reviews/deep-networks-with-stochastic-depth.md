# Deep Networks with Stochastic Depth

Gao Huang, Yu Sun, Zhuang Liu, Daniel Sedra, Kilian Weinberger, ArXiv, 2016

## Summary

This paper presents a way to reduce the expected network depth of deep residual networks during training by randomly dropping a subset of residual blocks and bypassing them with identity connections. The 'survival' probability p\_l decreases linearly with depth (from 1.0 to 0.5 at last layer) so as to keep layers that extract low-level features with higher probability. At test time, residual block functions are scaled by the expected number of times it appears during training, i.e. p\_l. This model achieves lower test errors than ResNets (with ReLU activations) on CIFAR-10, CIFAR-100 and SVHN.

## Strengths

- Shorter expected depth leads to faster training (>25% speedup).

- Helps reduce the vanishing gradient problem as shown by the mean gradient magnitude v/s epochs plot.

- Linear decay of survival probability works better than uniform survival, which supports the intuition that low-level features need to be reliably present.

- Stochastic depth acts as a regularizer. The 1202-layer stochastic depth residual network shows improvements over the 110-layer network, while the original ResNets paper reports overfitting and higher test error with 1000+ layers.

## Weaknesses / Notes

- Test errors for the updated ResNet architecture (ReLU activation inside residual function) are missing. That should perform better. Also, numbers on ImageNet.

- Stochastic depth can be interpreted as sequential ensembling as compared to parallel ensembles.

- It would be interesting to look at the filters learnt by stochastic depth residual networks, and to understand whether/how these networks learn hierarchical features as compared to the conventional CNN intuitions of compositionality.
