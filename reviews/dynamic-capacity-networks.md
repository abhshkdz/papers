# Dynamic Capacity Networks

Amjad Almahairi, Nicolas Ballas, Tim Cooijmans, Yin Zheng, Hugo Larochelle, Aaron Courville, ICML, 2016

## Summary

This paper presents a model that can dynamically split computation across coarse, low-capacity sub-networks and fine, high-capacity sub-networks. The coarse model processes the entire input data and is typically shallow while the fine model focuses on a few important regions of the input and is deeper. For images as input, this is a hard attention mechanism that can be trained with stochastic gradient descent and doesn't require a task-specific attention policy trained by reinforcement learning. Key ideas:

- A deep network h can be decomposed into bottom layers f and top layers g such that h(x) = g(f(x)). Further, f consists of two alternate sub-networks f\_c and f\_f. f\_c is a low-capacity sub-network while f\_f is a high-capacity sub-network.

- g should be able to use representations from f\_c and f\_f dynamically. f\_c processes the entire input while f\_f only a few important regions of the input.

- The coarse model processes the entire input and the norm of the gradient of the entropy with respect to the coarse vector at each spatial region is computed which is a measure of saliency. The use of the entropy gradient as a saliency measure encourages selecting input regions that could affect the uncertainty in the model’s predictions the most.

- The top-k input regions with highest saliency values are processed by the fine model. The refined representation for input to the top layers consists of both coarse and fine vectors. During backpropagation, gradients are computed for the refined model, i.e. propagating gradients at each position into either the coarse or fine features, depending on which was used.

- To make sure f\_c and f\_f representations are interchangeable and input to the top layers has smooth transitions, an additional objective term minimizes the squared distance between coarse and fine representations and this additional term is used only to optimize the coarse layers, not the fine layers.

- Experiments on cluttered MNIST, SVHN and comparison with RAM, DRAW and study with various values of number of patches for fine processing.

## Strengths

- Neat, general way to split computation based on importance of input; a hard-attention mechanism that can be trained with SGD, unlike RAM.

- Entropy gradient as a measure of saliency is an interesting idea, and it doesn't need labels i.e. can be used at test time.