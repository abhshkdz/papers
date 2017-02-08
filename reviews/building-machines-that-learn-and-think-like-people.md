# Building Machines That Learn and Think Like People

Brenden M. Lake, Tomer D. Ullman, Joshua B. Tenenbaum, Samuel J. Gershman, Behavioral and Brain Sciences, 2016

## Summary

This paper performs a comparitive study of recent advances in deep learning with human-like learning from a cognitive science point of view. Since natural intelligence is still the best form of intelligence, the authors list a core set of ingredients required to build machines that reason like humans.

- Cognitive capabilities present from childhood in humans.  
    - Intuitive physics; for example, a sense of plausibility of object trajectories, affordances.
    - Intuitive psychology; for example, goals and beliefs.
- Learning as rapid model-building (and not just pattern recognition).
    - Based on compositionality and learning-to-learn.
    - Humans learn by inferring a general schema to describe goals, object types and interactions. This enables learning from few examples. 
    - Humans also learn richer conceptual models.
        - Indicator: variety of functions supported by these models: classification, prediction, explanation, communication, action, imagination and composition.
        - Models should hence have strong inductive biases and domain knowledge built into them; structural sharing of concepts by compositional reuse of primitives.
- Use of both model-free and model-based learning.
    - Model-free, fast selection of actions in simple associative learning and discriminative tasks.
    - Model-based learning when a causal model has been built to plan future actions or maximize rewards.
- Selective attention, augmented working memory, and experience replay are low-level promising trends in deep learning inspired from cognitive psychology.
    - Need for higher-level aforementioned ingredients.
