# A simple neural network module for relational reasoning

Adam Santoro, David Raposo, David G.T. Barrett, Mateusz Malinowski, Razvan Pascanu, Peter Battaglia, Timothy Lillicrap, ArXiv, 2017

## Summary

This paper describes using Relation Networks (RN) for reasoning about relations between objects/entities.
RN is a plug-and-play module and although expects object representations as input,
the semantics of what an object is need not be specified, so object representations
can be convolutional layer feature vectors or entity embeddings from text, or something else.
And the feedforward network is free to discover relations between objects (as opposed to being
hand-assigned specific relations).

- At its core, RN has two parts:
	- a feedforward network `g` that operates on pairs of object representations,
	for all possible pairs, all pairwise computations pooled via element-wise addition
	- a feedforward network `f` that operates on pooled features for downstream
	task, everything being trained end-to-end

- When dealing with pixels (as in CLEVR experiment), individual object representations are
spatially distinct convolutional layer features (196 512-d object representations for VGG conv5 say).
The other experiment on CLEVR uses explicit factored object state representations with 3D coordinates,
shape, material, color, size.

- For bAbI, object representations are LSTM encodings of supporting sentences.

- For VQA tasks, `g` conditions its processing on question encoding as well, as relations
that are relevant for figuring out the answer would be question-dependent.


## Strengths

- Very simple idea, clearly explained, performs well. Somewhat shocked that it
hasn't been tried before.

## Weaknesses / Notes

Fairly simple idea — let a feedforward network
operate on all pairs of object representations and figure out relations
necessary for downstream task with end-to-end training. And it is fairly general in its design,
relations aren't hand-designed and neither are object representations — for
RGB images, these are spatially distinct convolutional layer features, for text,
these are LSTM encodings of supporting facts, and so on. This module can be dropped
in and combined with more sophisticated networks to improve performance at VQA.

RNs also offer an alternative design choice to prior works on CLEVR, that have
this explicit notion of programs or modules with specialized roles (that need to be pre-defined),
as opposed to letting these relations emerge, reducing dependency on hand-designing
modules and adding in inductive biases from an architectural point-of-view for
the network to reason about relations (earlier end-to-end VQA models didn't have
the capacity to figure out relations).
