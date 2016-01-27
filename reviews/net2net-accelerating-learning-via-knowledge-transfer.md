# Net2Net: Accelerating Learning via Knowledge Transfer

Tianqi Chen, Ian Goodfellow, Jonathon Shlens, ICLR, 2016

## Summary

This paper presents a simple method to accelerate the training
of larger neural networks by initializing them with parameters
from a trained, smaller network. Networks are made wider or deeper
while preserving the same output as the smaller network which
maintains performance when training starts, leading to faster
convergence. Main contributions:

- Net2Deeper
    - Initialize layers with identity weight matrices
    to preserve the same output.
    - Only works when activation function f satisfies
    f(If(x)) = f(x) for example ReLU, but not sigmoid, tanh.

- Net2Wider
    - Additional units in a layer are randomly sampled
    from existing units. Incoming weights are kept the same
    while outgoing weights are divided by the number of
    replicas of that unit so that the output at the next layer
    remains the same.

- Experiments on ImageNet
    - Net2Deeper and Net2Wider models converge faster to the
    same accuracy as networks initialized randomly.
    - A deeper and wider model initialized with Net2Net from
    the Inception model beats the validation accuracy (and
    converges faster).

## Strengths

- The Net2Net technique avoids the brief period of low performance that exists in
methods that initialize some layers of a deeper network from a trained
network and others randomly.

- This idea is very useful in production systems which essentially have to
be lifelong learning systems. Net2Net presents an easy way to immediately
shift to a model of higher capacity and reuse trained networks.

- Simple idea, clearly presented.


## Weaknesses / Notes

- The random mapping algorithm for different layers was done manually
for this paper. Developing a remapping inference algorithm should be
the next step in making the Net2Net technique more general.

- The final accuracy that Net2Net models achieve seems to depend only
on the model capacity and not the initialization. I think this merits
further investigation. In this paper, it might just be because of randomness
in training (dropout) or noise added to the weights of the new units to
approximately represent the same function (when not using dropout).