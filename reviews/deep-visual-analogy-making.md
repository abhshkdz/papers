# Deep Visual Analogy-Making

Scott E. Reed, Yi Zhang, Yuting Zhang, Honglak Lee, NIPS, 2015

## Summary

This paper introduces an end-to-end trainable neural model capable of performing analogical reasoning in image representations followed by decoding back to image space. Specifically, given a 4-tuple A:B::C:D, the task is to apply the transformation A:B to C. The motivation is clear — humans are excellent at generalizing to hypothetical transformations about images ("what if this chair were rotated 30 degrees clockwise?").

- The objective function follows directly from vector addition: `MSE(d - g(f(b) - f(a) + f(c)))` where `f` and `g` are convolutional neural networks.

- In case of rotation, a purely additive transformation is not optimal because repeated application of this transformation to the same query image will never return to the original point. Instead, multiplicative interactions or MLPs are used to condition the transformation on `c` as well.

- Analogy-making is also performed on disentangled representations, which separate factors of variation to separate coordinates and are learnt from distinct images `a`, `b`, `c` such that the objective is `MSE(c - g(s . f(a) + (1-s) . f(b)))` where `s` are switch variables to disentangle features. Disentangled image features allow the analogy-making model to traverse the manifold of a given factor or subset of factors.

- Experiments on transforming shapes, generating 2D video game sprites and 3D car renderings.

## Strengths

- Neat idea, well-presented