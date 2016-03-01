# Stacked Attention Networks for Image Question Answering

Zichao Yang, Xiaodong He, Jianfeng Gao, Li Deng, Alex Smola, ArXiv, 2015

## Summary

This paper introduces a Stacked Attention Network (SAN) for visual question answering.
SAN uses a multiple layer attention mechanism that uses the semantic question representation
to query the image and locate relevant visual regions, and to infer the answer.
Details of the SAN model:

- Image features are extracted from the last pooling layer of a deep CNN (like VGG-net).
    - Input images are first scaled to 448 x 448, so at the last pooling layer, features
    have the dimension 14 x 14 x 512 i.e. 512-dimensional vectors at each image location
    with a receptive field of 32 x 32 in input pixel space.

- Question features are the last hidden state of the LSTM.
    - Words are one-hot encoded, transferred to a vector space by passing through an
    embedding matrix and these word vectors are fed into the LSTM at each time step.

- Image and question features are combined into a query vector to locate relevant visual regions.
    - Both the LSTM hidden state and 512-d image feature vector at each location are transferred
    to the same dimensionality (say k) by a fully connected layer, and added and passed through
    a non-linearity (tanh).
    - Each k-dimensional feature vector is then transformed down to a single scalar and
    a softmax is taken over all image regions to get the attention distribution (say p\_{I}).
    - This attention distribution is used to weight the pooling layer visual features (\sum_{i}p\_{i}v\_{i})
    and added to the LSTM vector to get a new query vector.
    - In subsequent attention layers, this updated query vector is used to repeat the same process
    of getting an attention distribution.
    - The final query vector is used to compute a softmax over the answers.

## Strengths

- The multi-layer attention mechanism makes sense intuitively and the qualitative results
somewhat indicate that going from the first attention layer to subsequent attention layers,
the network is able to focus on fine-grained visual regions as it discovers relationships
among multiple objects ('what are sitting in the basket on a bicycle').

- SAN benefits VQA, they demonstrate state-of-the-art accuracies on multiple datasets, with
question-type breakdown as well.

## Weaknesses / Notes

- Right now, the attention distribution is learnt in an unsupervised manner by the network.
It would be interesting to think about adding supervisory attention signal. Another way to
improve accuracies would be to use deeper LSTMs.
