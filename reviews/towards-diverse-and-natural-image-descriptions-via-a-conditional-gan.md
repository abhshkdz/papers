# Towards Diverse and Natural Image Descriptions via a Conditional GAN

Bo Dai, Sanja Fidler, Raquel Urtasun, Dahua Lin, ICCV, 2017

## Summary

This paper proposes a conditional GAN-based image captioning model.
Given an image, the generator generates a caption, and given an image
and caption, the discriminator/evaluator distinguishes between generated
and real captions. Key ideas:

- Since caption generation involves sequential sampling, which is
non-differentiable, the model is trained with policy gradients, with
the action being the choice of word at every time step, policy being
the distribution over words, and reward the score assigned by the
evaluator to generated caption.

- The evaluator's role assumes a completely generated caption as input
(along with image), which in practice leads to convergence issues. Thus
to accommodate feedback for partial sequences during training, Monte Carlo
rollouts are used, i.e. given a partial generated sequence, n completions
are sampled and run through the evaluator to compute reward.

- The evaluator's objective function consists of three terms
    - image-caption pairs from training data (positive)
    - image and generated captions (negative)
    - image and sampled captions for other images from training data (negative)

- Both the generator and evaluator are pretrained with supervision / MLE, then
fine-tuned with policy gradients. During inference, evaluator score is used as
the beam search objective.

## Strengths

This is neat paper with insightful ideas (Monte Carlo rollouts for assigning
rewards to partial sequences, evaluator score as beam search objective),
and is perhaps the first work on C-GAN-based image captioning.

## Weaknesses / Notes
