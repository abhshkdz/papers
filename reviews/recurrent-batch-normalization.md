# Recurrent Batch Normalization

Tim Cooijmans, Nicolas Ballas, César Laurent, Aaron Courville, ArXiv, 2016

## Summary

This paper presents a re-parameterization of the LSTM to successfully apply batch normalization, which results in faster convergence and improved generalization on a several sequential tasks. Main contributions:

- Batch normalization is applied to the input to hidden and hidden to hidden projections.
    - Separate statistics are maintained for each timestep, estimated over each minibatch during training and over the whole dataset during test.
    - For generalization to longer sequences during test time, population statistics of time T\_max are used for all time steps beyond it.
    - The cell state is left untouched so as not to hinder the gradient flow.

- Proper initialization of batch normalization parameters to avoid vanishing gradients.
    - They plot norm of gradient of loss wrt hidden state at different time steps for different BN variance initializations. High variance (\gamma = 1) causes gradients to die quickly by driving activations to the saturation region.
    - Initializing BN variance to 0.1 works well.

## Strengths

- Simple idea, the authors finally got it to work. Proper initialization of BN parameters and maintaining separate estimates for each time step play a key role.

## Weaknesses / Notes

- It would be useful in practice to put down a proper formulation for using batch normalization with variable-length training sequences.