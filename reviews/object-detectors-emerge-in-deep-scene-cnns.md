# Object Detectors Emerge in Deep Scene CNNs

Bolei Zhou, Aditya Khosla, Agata Lapedriza, Aude Oliva, Antonio Torralba, ICLR, 2015

## Summary

This paper hypothesizes that a CNN trained for scene classification automatically
discovers meaningful object detectors, representative of the scene categories,
without any explicit object-level supervision. This claim is backed by well-designed
experiments which are a natural extension of the primary insight that since scenes
are composed of objects (a typical bedroom would have a bed, lamp; art gallery would
have paintings, etc), a CNN that performs reasonable well on scene recognition
must be localizing objects in intermediate layers.

## Strengths

- Demonstrates the difference in learned representations in Places-CNN and ImageNet-CNN.
    - The top 100 images that have the largest average activation per layer are picked and it's shown that earlier layers such as pool1 prefer similar images for both networks while deeper layers tend to be more specialized to the specific task of scene or object categorization i.e. ~75% of the top 100 images that show high activations for fc7 belong to ImageNet for ImageNet-CNN and Places for Places-CNN.
- Simplifies input images to identify salient regions for classification.
    - The input image is simplified by iteratively removing segments that cause the least decrease in classification score until the image is incorrectly classified. This leads them to the minimal image representation (sufficient and necessary) that is needed by the network to correctly recognize scenes, and many of these contain objects that provide discriminative information for scene classification.
- Visualizes the 'empirical receptive fields' of units.
    - The top K images with highest activations for a given unit are identified. To identify which regions of the image lead to high unit activations, the image is replicated with occluders at different regions. The occluded images are passed through the network and large changes in activation indicate important regions. This leads them to generate feature maps and finally to empirical receptive fields after appropriate centre-calibration, which are more localized and smaller than the theoretical size.
- Studies the visual concepts / semantics captured by units.
    - AMT workers are surveyed on the segments that maximally activate units. They're asked to tag the visual concept, mark negative samples and provide the level of abstraction (from simple elements and colors to objects and scenes). Plot of distribution of semantic categories at each layer shows that deeper layers do capture higher levels of abstraction and Places-CNN units indeed discover more objects than ImageNet-CNN units.

## Weaknesses / Notes

- Unclear as to how they obtain soft, grayed out images from the iterative segmentation methodology in the first approach where they generate minimal image representations needed for accurate classification. I would assume these regions to be segmentations with black backgrounds and hard boundaries. Perez et al. (2013) might have details regarding this.