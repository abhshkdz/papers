# You Only Look Once: Unified, Real-Time Object Detection

Joseph Redmon, Santosh Divvala, Ross Girshick, Ali Farhadi, ArXiv15

## Summary

This paper models object detection as a regression problem for bounding
boxes and object class probabilities with a single pass through the CNN. The
main contribution is the idea of dividing the image into a 7x7 grid, and having
each cell predict a distribution over class labels as well as a bounding box
for the object whose center falls into it. It's much faster than R-CNN and
Fast R-CNN, as the additional step of extracting region proposals has been
removed.

## Strengths

- Works real-time. Base model runs at 45fps and a faster version goes up to
150fps, and they claim that it's more than twice as fast as other works on
real-time detection.

- End-to-end model; Localization and classification errors can be jointly
optimized.

- YOLO makes more localization errors and fewer background mistakes than
Fast R-CNN, so using YOLO to eliminate false background detections from
Fast R-CNN results in ~3% mAP gain (without much computational time as R-CNN
is much slower).

## Weaknesses / Notes

- Results fall short of state-of-the-art: 57.9% v/s 70.4% mAP (Faster R-CNN).

- Performs worse at detecting small objects, as at most one object per grid
cell can be detected.