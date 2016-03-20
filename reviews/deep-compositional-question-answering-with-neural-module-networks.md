# Deep Compositional Question Answering with Neural Module Networks

Jacob Andreas, Marcus Rohrbach, Trevor Darrell, Dan Klein, CVPR, 2016

## Summary

This paper presents an approach to visual question answering by dynamically composing networks of independent neural modules based on the semantic parsing of the question. Main contributions:

- Independent neural modules that can be combined together and jointly trained.
    - Attention: Convolutional layer, with different filters for different instances. For example, attend[dog], attend[cat], etc.
    - Re-attention: FC-ReLU-FC-ReLU, weights are different for different instances. For example, re-attend[above], re-attend[not], etc.
    - Combination: Stacks two attention maps, followed by conv-ReLU to map to a single attention map. For example, combine[and], combine[except], etc.
    - Classification: Combines attention map and image, followed by FC-Softmax to map to answer. For example, classify[colors].
    - Measurement: FC-ReLU-FC-Softmax, takes attention map as input. For example, measure[exists].

- Structured representations are extracted from questions and these are then mapped to network layouts, including the connections between them.
    - All leaves become attend modules, all internal nodes become re-attend or combine modules dependent on their arity, and root nodes become measure modules for yes/no questions and classify modules for all other question types.
    - Networks with the same structure but different instantiations can be processed in the same batch. For example, classify[color]\(attend[cat]\), classify[where]\(attend[truck]\).

- Predictions from the module network are combined with LSTM representations to get the final answer.
    - Syntactic regularities: 'what is flying?' and 'what are flying?' get mapped to the same module network.
    - Semantic regularities: 'green' is an implausible answer for 'what color is the bear?'.

- Experiments are performed on the synthetic SHAPES dataset and VQA dataset.
    - Performance on the SHAPES dataset is better as it is designed to benefit from compositionality.

## Strengths

- This model takes advantage of the inherently compositional property of language, which makes a lot of sense. VQA is an extremely complex task and breaking it up into separate functions/modules is an excellent approach.

## Weaknesses / Notes

- Mapping from syntactic structure to module network is hand-designed. Ideally, the model should learn this too to generalize.

- Due to its compositional nature, this kind of model can possibly be used in the zero-shot learning setting, i.e. generalize to novel question types that the network hasn't seen before.