# Deep Reinforcement Learning for Dialogue Generation

Jiwei Li, Will Monroe, Alan Ritter, Michel Galley, Jianfeng Gao, Dan Jurafsky, ArXiv, 2016

## Summary

This paper builds on top of a bunch of existing ideas for building neural conversational agents so as to control against generic and repetitive responses. 

Their model is the sequence-to-sequence model with attention (Bahdanau et al.), first trained with the usual MLE loss and fine-tuned with policy gradients to optimize for specific conversational properties. Specifically, they define 3 rewards:

1. Ease of answering — Measured as the likelihood of responding to a query with a list of hand-picked dull responses (more negative log likelihood is higher reward). 
2. Information flow — Consecutive responses from the same agent (person) should have different information, measured as negative of log cosine distance (more negative is better).
3. Semantic coherence — Mutual information between source and target (the response should make sense wrt query). P(a|q) + P(q|a) where a is answer, q is question.

The model is pre-trained with the usual supervised objective function, taking source as concatenation of two previous utterances. Then they have two stages of policy gradient training, first with just a mutual information reward and then with a combination of all three. The policy network (sequence-to-sequence model) produces a probability distribution over actions (responses) given state (previous utterances). To estimate the gradient in an iteration, the network is frozen and responses are sampled from the model, the rewards for which are then averaged and gradients are computed for first L tokens of response using MLE and remaining T-L tokens with policy gradients, with L being gradually annealed to zero (moving towards just the long-term reward).

Evaluation is done based on length of dialogue, diversity (distinct unigram, bigrams) and human studies on

1. Which of two outputs has better quality (single turn)
2. Which of two outputs is easier to respond to, and
3. Which of two conversations have better quality (multi turn).

## Strengths

- Interesting results
    - Avoids generic responses
    - 'Ease of responding' reward encourages responses to be question-like
- Adding in hand-engineereed approximate reward functions based on conversational properties and using those to fine-tune a pre-trained network using policy gradients is neat.
- Policy gradient training also encourages two dialogue agents to interact with each other and explore the complete action space (space of responses), which seems desirable to identify modes of the distribution and not converge on a single, high-scoring, generic response.

## Weaknesses / Notes

- Evaluating conversational agents is hard. BLEU / perplexity are intentionally avoided as they don't necessarily reward desirable conversational properties.