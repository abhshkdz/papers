# Convolutional Neural Networks for Sentence Classification

Yoon Kim, EMNLP, 2014

## Summary

This paper reports on a series of experiments with CNNs trained
on top of pre-trained word vectors for sentence-level classification
tasks. The model achieves very good performance across datasets, and
state-of-the-art on a few. The proposed model has an input layer
comprising of concatenated 'word2vec' embeddings, followed by a single
convolutional layer with multiple filters, max-pooling over time,
fully connected layers and softmax. They also experiment with static
and non-static channels which basically implies whether they finetune
word2vec embeddings or not.

## Strengths

- Very simple yet powerful model formulation, which achieves really good
performance across datasets.

- The different model formulations drive home the point that initializing
input vectors with word2vec embeddings is better than random initializations.
Finetuning these embeddings for the task leads to further improvements over
static embeddings.

## Weaknesses / Notes

- No intuition as to why the model with both static and non-static channels
gives mixed results.

- They briefly mention that they experimented with SENNA embeddings which lead
to worse results although no quantitative results are provided. It would have been
interesting to have a comparative study with GloVe embeddings as well.