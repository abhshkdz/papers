# World Models

David Ha, Jürgen Schmidhuber, ArXiv, 2018

## Summary

This paper presents an approach to build a task-agnostic generative model of the
environment, and use it to train an agent's policy to do well at the task. The
core components of the model include:

- VAE-based world model V, that encodes image observations to a latent z,
and also enables sampling z at test time and inverting it to get corresponding pixels.

- LSTM + Mixture Density network M that temporally integrates z; takes previous z, previous action as input
and predicts parameters of a mixture of Gaussians distribution used to sample the next z.

- Policy network C, which consists of a single fully-connected layer from [z h] to
a softmax distribution over actions.

- Training is stage-wise; V is first trained to encode frames, then M is trained to
model P(z_{t+1} | a_t, z_t, h_t), and finally C is trained using CMA-ES.

- Experiments are performed in Car Racing and VizDoom: Take Cover environments.
    - For VizDoom, the authors also experiments with training solely using sampled z vectors as a
    "dreamt up" interface and then transfering to the actual environment, and show that
    training within the hallucinated environment with high temperature / uncertainty
    leads to a better-performing and low variance policy when transfered to the actual environment.

- The authors discuss how C having access to M's hidden state can lead to exploitation
of some edge cases / adversarial behavior, wherein the agent learns that when training
within predicted Z, certain actions can lead to magically extinguishing incoming bullets,
which is interesting and not too unexpected.

## Strengths

- This is neat, well-written paper with a cool idea, that cleanly separates building
a world model from downstream task / policy, and demonstrates that having a fairly shallow
policy network over a large world model can work pretty well for some of these tasks.

- The related work section is a gold mine. :)

## Weaknesses / Notes

- It's not immediately obvious how generalizeable features learnt in an unsupervised
manner are. Whenever downstream task annotations are available, using those should
definitely lead to better features wherein the model can decide which parts of the visual
input are relevant for the task.