# Residual Networks are Exponential Ensembles of Relatively Shallow Networks

Andreas Veit, Michael Wilber, Serge Belongie, ArXiv, 2016

## Summary

This paper introduces an interpretation of deep residual networks as implicit ensembles of exponentially many shallow networks. For a residual block i, there are 2^{i-1} paths from input to i, and the input to i is a mixture of 2^{i-1} different distributions. The interpretation is backed by a number of experiments such as removing or re-ordering residual blocks at test time and plotting norm of gradient v/s number of residual blocks the gradient signal passes through. Removing k residual blocks (for k <= 20) from a network of depth n decreases the number of paths to 2^{n-k} but there are still sufficiently many valid paths to not hurt classification error, whereas sequential CNNs have a single viable path which gets corrupted. Plot of gradient at input v/s path length shows that almost all contributions to the gradient come from paths shorter than 20 residual blocks, which are the effective paths. The paper concludes by saying that network 'multiplicity', which is the number of paths, plays a key role in terms of the network's expressability.

## Strengths

- Extremely insightful set of experiments. These experiments nail down the intuitions as to why residual networks work, as well as clarify the connections with stochastic depth (sampling the network multiplicity during training i.e. ensemble by training) and highway networks (reduction in number of available paths by gating both skip connections and paths through residual blocks).

## Weaknesses / Notes

- Connections between effective paths and model compression.