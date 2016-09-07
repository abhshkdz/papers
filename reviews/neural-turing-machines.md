# Neural Turing Machines

Alex Graves, Greg Wayne, Ivo Danihelka, ArXiv, 2014

## Summary

Neural Turing Machine (NTM) consists of a neural network controller interacting with a working memory bank in a learnable manner. This is analogous to computers — controllers = CPU (hidden activations as registers) and memory matrix = RAM. Key ideas:

- Controller (modified RNN) interacts with external world via input and output vectors, and with memory via read and write "heads"

- "Read" vector is a convex combination of row-vectors of M_t (memory matrix at time t) — r\_t = \sum w\_t(i) M\_t(i) where w_t is a vector of weightings over N memory locations

- "Writing" is decomposed into 1) erasing and 2) adding
    - The write head produces the erase vector e_t and the add vector a_t along with the vector of weightings over memory locations w_t
    - M\_t(i) = M\_{t-1}(i)[1 - w_t(i) e_t] + w\_t(i) a\_t
    - Erase and add vectors control which components of memory are updated, while weightings w_t control which locations are updated

- Weight vectors are produced by an addressing mechanism
    - Content-based addressing
        - Each head produces length M key k_t that is compared to each vector M_t(i) by cosine similarity and a temperature parameter. The weightings are normalized (softmax).

    - Location-based addressing
        - Interpolation: Each head produces interpolation gate g_t that is used to blend between weighting at previous time step and the content weighting of current tilmestep w^{g}\_t = g\_t w^{c}\_t + (1-g\_t)w\_{t-1}
        - Shift: Circular convolution (modulo N) with a shift weighting distribution, for example softmax over integer shift positions (say 3 locations)
        - Sharpening: Each head emits \gamma_t to sharpen the final weighting

- Experiments on copy, repeat-copy, associative memory, N-gram emulator and priority sort

## Links

- [Attention and Augmented RNNs](http://distill.pub/2016/augmented-rnns/)
- [NTM-Lasagne](https://medium.com/snips-ai/ntm-lasagne-a-library-for-neural-turing-machines-in-lasagne-2cdce6837315)
