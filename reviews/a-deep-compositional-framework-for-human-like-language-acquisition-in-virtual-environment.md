# A Deep Compositional Framework for Human-like Language Acquisition in Virtual Environment

Haonan Yu, Haichao Zhang, Wei Xu, ArXiv, 2017

## Summary

This paper proposes a framework where an agent learns to navigate a 2D maze-like
environment (XWORLD) from (templated) natural language commands, in the process
simultaneously learning visual representations, syntax and semantics of language and
performing navigation actions. The task is essentially VQA + navigation; at every step
the agent either gets a question about the environment or navigation command,
and the output is either a navigation action or answer. Key contributions:

- Grounding and recognition are tied together to be two versions of the same problem.
In grounding, given an image feature map and label (word), the problem is to find
regions of the image corresponding to word semantics (attention map); and in
recognition, given an image feature map and attention, the problem is to assign
a word label. And thus word embeddings (for grounding) and softmax layer weights
(for recognition) are tied together. This enables transferring concepts
learnt during recognition to navigation.
	- Further, recognition is modulated by question intent. For e.g. given an
	attention map that highlights an agent's west, should it be recognized as
	'west', 'apple' or 'red' (location, object or attribute)? It depends on what
	the question asks. Thus, GRU encoding of question produces an embedding mask
	that modulates recognition. The equivalent when grounding is that word embeddings
	are passed through fully-connected layers.

- Compositionality in language is exploited by performing grounding and
recognition by sequentially (softly) attending to parts of a sentence and
grounding in image. The resulting attention map is selectively combined
with attention from previous timesteps for final decision.

## Weaknesses / Notes

Although the environment is super simple, it's a neat framework and it is useful
that the target is specified in natural language (unlike prior/concurrent work
e.g. Zhu et al., ICRA17). The model gets to see a top-down centred view of the
entire environment at all times, which is a little weird.
