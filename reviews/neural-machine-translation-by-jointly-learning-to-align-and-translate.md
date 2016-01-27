# Neural Machine Translation by Jointly Learning to Align and Translate

Dzmitry Bahdanau, Kyunghyun Cho, Yoshua Bengio, ICLR, 2015

## Summary

This paper introduces an attention mechanism (soft memory access)
for the task of neural machine translation. Qualitative and quantitative
results show that not only does their model achieve state-of-the-art BLEU
scores, it performs significantly well for long sentences which was a
drawback in earlier NMT works. Their motivation comes from the fact that
encoding all information from an input sentence into a single fixed length
vector and using that in the decoder was probably a bottleneck. Instead,
their decoder uses an attention vector, which is a weighted sum of the
input hidden states, and is learned jointly. Main contributions:

- The encoder is a bidirectional RNN, in which they take the annotation
of each word to be the concatenation of the forward and backward RNN states.
The idea is that the hidden state should encode information from both the
previous and following words.

- The proposed attention mechanism is a weighted sum of the input hidden
states, the weights for which come from an attention function (a single-layer
perceptron, which takes as input the previous hidden state of the decoder and
the current word annotation from the encoder) and are softmax-normalized.

## Strengths

- Incorporating the attention mechanism shows large improvements on
longer sentences. The attention matrix is easily interpretable as well,
and visualizations in the paper show that higher weights are being assigned
to input words that correspond to output words irrespective of their order
in the sequence (unlike an attention model that uses a mixture of Gaussians
which is monotonic).

## Weaknesses / Notes

- Their model formulation to capture long-term dependencies is far more
principled than Sutskever et al's inverting the input idea. They should
have done a comparative study with their approach as well though.