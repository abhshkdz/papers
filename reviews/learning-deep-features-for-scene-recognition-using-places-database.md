# Learning Deep Features for Scene Recognition using Places Database

Bolei Zhou, Agata Lapedriza, Jianxiong Xiao, Antonio Torralba, Aude Oliva

## Summary

This paper introduces the Places dataset, which is a scene-centric
dataset at the scale of ImageNet (which is for object recognition)
so as to enable training of deep CNNs like AlexNet, and achieves
state-of-the-art for scene benchmarks. Main contributions:

- Collects a dataset at ImageNet scale for scene recognition.
- Achieves state-of-the-art on scene benchmarks: SUN397, MIT Indoor67, Scene15, SUN Attribute.
- Introduces measures for comparing datasets: density and diversity.
- Makes a thorough comparison b/w ImageNet and Places, from dataset to classification results to learned representation visualizations.

## Strengths

- Relative density and diversity are neat ideas for comparing datasets, and are backed by AMT experiments.
    - Relative density: The more visually similar a nearest neighbour is to a randomly sampled image from a dataset, the more dense it is.
    - Relative diversity: The more visually similar two randomly sampled images from a dataset are, the less diverse it is.
- Demonstrates via activation and mean image visualizations that different representations are learned by CNNs trained on ImageNet and Places
    - Conv1 layer visualizations can be directly seen, and are similar for ImageNet-CNN and Places-CNN. They capture low-level information like oriented edges and colors.
    - For higher layers, they visualize the average of top 100 images that maximize activations per unit. As we go deeper, ImageNet-CNN units have receptive fields that look more like object-blobs and Places-CNN have RFs that look more like landscapes with spatial structures.

## Weaknesses / Notes

- No explanation as to why the model trained on ImageNet and Places combined (minus overlapping images) performs better than ImageNet-CNN or Places-CNN on some benchmarks and worse on others.