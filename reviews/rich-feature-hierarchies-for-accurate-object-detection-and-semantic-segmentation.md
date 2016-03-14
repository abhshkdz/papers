# Rich Feature Hierarchies for Accurate Object Detection and Semantic Segmentation

Ross Girshick, Jeff Donahue, Trevor Darrell, Jitendra Malik, CVPR, 2014

## Summary

This paper presents R-CNN, an approach to do object detection using CNNs pre-trained for image classification. Object proposals are extracted from the image using Selective Search, dilated by few pixels, warped to CNN input size and fed into the CNN to extract features (they experiment with pool5, fc6, fc7). These extracted feature vectors are scored using SVMs, one per class. Bounding box regression, where they predict parameters to move the proposal closer to ground-truth, further boosts localization.

The authors use AlexNet, pre-trained on ImageNet and finetuned for detection. Object proposals with IOU overlap greater than 0.5 are treated as positive examples, and others as negative, and a 21-way classification (20 object categories + background) is set up to finetune the CNN. After finetuning, SVMs are trained per class, taking only the ground-truth boxes as positives, and IOU <= 0.3 as negatives.

R-CNN achieves major performance improvements on PASCAL VOC 2007/2010 and ILSVRC2013 detection datasets. Finally, this method is extended to do semantic segmentation and achieves competitive results.

## Strengths

- The method is simple and effective.
- Extensive ablation studies show why R-CNN works.
    - FC7 is the best feature to use (against pool5, fc6).
    - Fine-tuning provides a large boost in performance.
    - VGG performs better than AlexNet.
    - Bounding box regression further improves localization.

## Weaknesses / Notes

- Each region proposal is treated independently, which adds up to compute time.
- There are lots of different parts; the network can't be trained end-to-end.