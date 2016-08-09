# Actions ~ Transformations

Xiaolong Wang, Ali Farhadi, Abhinav Gupta, CVPR, 2016

## Summary

This paper introduces a novel representation for actions in videos as transformations that change the state of the environment from what it was before the action (precondition) to what it will be after it (effect).

- Model
    - The model utilizes a Siamese architecture with each head having convolutional and fully-connected layers (similar to VGG16). Each head extracts features for a subset of video frames (precondition or effect) that are aggregated by average pooling and followed by a fully-connected layer.
    - The precondition frames are indexed from 1 to z\_p and the effect frames from z\_e to t. Both z\_p and z\_e are latent variables, constrained to be from [1/3t, 1/2t] and [1/2t, 2/3t] respectively and estimated via brute force search during training.
    - The action is represented as a linear transformation between the final fully-connected layers of the two heads. For n action categories, the transformation layer has n transformation matrices.
    - The model is trained with a contrastive loss function to 1) maximize cosine similarity between the effect embedding and the transformed precondition embedding, and 2) maximize distance for incorrect transformations if greater than a chosen margin.
- ACT Dataset
    - 50 keywords, 43 classes, ~500 YouTube videos per keyword.
    - The authors collect the ACT dataset primarily for the task of cross-category generalization (as it doesn't allow models to overfit to contextual information). For example, how would a model learned on "opening a window" generalize to recognize "opening the trunk of the car"? How about generalizing from a model trained on "climbing a cliff" to recognize "climbing a tree"?
    - The ACT dataset has class and super-class annotations from human workers. Each super-class has different sub-categories which are the same action under different subjects, objects and scenes.
- Experiments
    - Action recognition on UCF101, HMDB51, ACT.
    - Cross-category generalization on ACT.
- Visualizations
    - Nearest neighbor: modeling the actions as transformations gives semantically meaningful retrievals that don't just depend on motion and color.
    - Gradient visualizations (Simonyan et al. 2014): model focuses on changes in scene (human + object) than context.
    - Embedding retrievals based on transformed precondition embeddings.

## Strengths

- Modeling action as a transformation from precondition to effect is a very neat idea.
- The exact formulation and supporting experiments and ablation studies are thorough.

## Weaknesses / Notes

- During inference, the model first extracts features for all frames and then does a brute force search over (y,z\_p,z\_e) to estimate the action category and segmentation into precondition and effect. For longer sequences, this seems expensive. Although hard decisions aren't differentiable, a soft attention mechanism on z might be feasible and reduce computation to a single forward pass.