# Faster R-CNN: Towards Real-Time Object Detection with Region Proposal Networks

## References
* [Github](https://github.com/rbgirshick/py-faster-rcnn)
* [Paper](https://arxiv.org/pdf/1506.01497.pdf)

## Abstract
- In this work, **we introduce a Region Proposal Network (RPN)** that shares full-image convolutional features with the detection network, thus enabling nearly **cost-free region proposals**.
- An RPN is a fully convolutional network that simultaneously predicts object bounds and objectness scores at each position.
- The RPN is trained end-to-end to generate high-quality region proposals, which are used by Fast R-CNN for detection.
- We further merge RPN and Fast R-CNN into a single network by sharing their convolutional features:
    - Attention mechanisms tells the unified network where to look.

## Introduction
In contrast to prevalent methods that uses, pyramids of images or pyramids of filters, we introduce novel **anchor boxes** that serve as references at multiple scales and aspect ratios.

To unify RPNs with Fast R-CNN object detection networks, we propose a training scheme that alternates between fine-tuning for the region proposal task and then fine-tuning for object detection, while keeping the proposals fixed.
    - This scheme converges quickly and produces a unified network with convolutional features that are shared between both tasks.

## Faster R-CNN
Our object detection system, called Faster R-CNN, is composed of two modules:
1. Deep fully convolutional network that proposes regions.
2. Fast R-CNN detector that uses the proposed regions.

The entire system is a single, unified network for object detection:
```mmd
graph LR;
  a(Image) --->|Conv Layers| b(Feature Maps) -->|Reason Proposal<br>Network| c(Proposals) -->|RoI Pooling| d(Detections) -->|Classification| e(Objects Class);
```

### Region Proposal Network
```mmd
graph LR;
  a(Image<br>of any size) -->|Region Proposal Network| b(Set of rectangular object proposals,<br>each with an objectness score);
```

- To generate region proposals, we slide a small network over the convolutional feature map output by the last shared convolutional layer.
    - This small network takes as input an n x n spatial window of the input convolutional feature map. (n=3 is used in this paper)
    - Each sliding window is mapped to a lower-dimensional feature.
    - This feature is fed into two sibling fullyconnected layers:
        1. A box-regression layer (reg)
        2. A box-classification layer (cls).
    - **Note:** Because the mini-network operates in a sliding-window fashion, the fully-connected layers are shared across all spatial locations.

#### Anchors

