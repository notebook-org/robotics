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
- At each sliding-window location, we simultaneously predict multiple region proposals, where the number of maximum possible proposals for each location is denoted as k.
    - So,
        1. reg layer: 4k outputs encoding the coordinates of k boxes
        2. cls layer: outputs 2k scores that estimate probability of object or not object
    -  for each proposal.
- The k proposals are parameterized relative to k reference boxes, which we call **anchors**.
    - An anchor is centered at the sliding window in question, and is associated with a scale and aspect ratio.
    - By default we use 3 scales and 3 aspect ratios, yielding k = 9 anchors at each sliding position.
    - For a convolutional feature map of a size W x H, there are WHk anchors in total.

##### Translation-Invariant Anchors
**Translation Invariant:** If one translates an object in an image, the proposal should translate and the same function should be able to predict the proposal in either location.

##### Multi-Scale Anchors as Regression References
There have been two popular ways for multi-scale predictions:
1. Based on image/feature pyramids.
   - The images are resized at multiple scales, and feature maps are computed for each scale.
   - This way is often useful but is time-consuming.
2. Sliding windows of multiple scales (and/or aspect ratios) on the feature maps.
   -  It can be thought of as a pyramid of filters.

#### Loss Function
For training RPNs, we assign a binary class label (of being an object or not) to each anchor.

We assign a positive label to two kinds of anchors:
1. The anchor/anchors with the highest Intersection-overUnion (IoU) overlap with a ground-truth box.
2. An anchor that has an IoU overlap higher than 0.7 with any ground-truth box.

We assign a negative label to a non-positive anchor if its IoU ratio is lower than 0.3 for all ground-truth boxes.

Anchors that are neither positive nor negative do not contribute to the training objective.

With these definitions, we minimize an objective function following the multi-task loss in Fast R-CNN:

$$L(p_i, t_i) = \frac{1}{N_{cls}} \sum_{i} L_{cls}(p_i, p_i^{\star}) + \lambda \frac{1}{N_{reg}} p_i^{\star} L_{reg}(t_i, t_i^{\star})$$

where,
- $i$ is the index of an anchor in a mini-batch.
- $p_i$ is the predicted probability of anchor i being an object.
- $p_i^{\star}$ is 1 if the anchor is positive, and zero if anchor is negative.
- $t_i$ is a vector representing the 4 parameterized coordinates of the predicted bounding box.
- $t_i^{\star}$ is that of the ground-truth box associated with a positive anchor.
- $L_{cls}$ is the log loss over two classes (object vs not object).
- $L_{reg}(t_i, t_i^{\star}) = R(t_i, t_i^{\star})$, where R is the robust loss function (L1 Smooth).

For bounding box regression,
$$t_x = \frac{x - x_a}{w_a},
t_y = \frac{y - y_a}{h_a},
t_w = \log(\frac{w}{w_a}),
t_h = \log(\frac{h}{h_a})$$

$$t_x^{\star} = \frac{x^{\star} - x_a}{w_a},
t_y^{\star} = \frac{y^{\star} - y_a}{h_a},
t_w^{\star} = \log(\frac{w^{\star}}{w_a}),
t_h^{\star} = \log(\frac{h^{\star}}{h_a})$$

- $x$, $y$, $w$, & $h$ denote the box's center coordinates and its width and height.
- Variables $x$, $x_a$, and $x^{\star}$ are for the predicted box, anchor box, and groundtruth box respectively (likewise for $y, w, h$).

- This can be thought of as bounding-box regression from an anchor box to a nearby ground-truth box.
- Features used for regression are of the same spatial size (3 x 3) on the feature maps.
- To account for varying sizes, a set of k bounding-box regressors are learned. 
- Each regressor is responsible for one scale and one aspect ratio, and the k regressors do not share weights.

#### Training RPNs
The RPN can be trained end-to-end by backpropagation and stochastic gradient descent.

- We follow the image-centric sampling strategy from to train this network.
- Each mini-batch arises from a single image that contains many positive and negative example anchors.
- We randomly sample 256 anchors in an image to compute the loss function of a mini-batch, where the sampled positive and negative anchors have a ratio of up to 1:1.
    - If there are fewer than 128 positive samples in an image, we pad the mini-batch with negative ones.
- We randomly initialize all new layers by drawing weights from a zero-mean Gaussian distribution with standard deviation 0.01.
- All other layers (i.e., the shared convolutional layers) are initialized by pretraining a model for ImageNet classification.

- Learning rate: 0.001 for 60k mini-batches and 0.0001 for the next 20k mini-batches on the PASCAL VOC dataset.
- momentum: 0.9
- weight_decay: 0.0005

### Sharing Features for RPNs and Fast R-CNN
Next we describe algorithms that learn a unified network composed of RPN and Fast R-CNN with shared convolutional layers.

- Both RPN and Fast R-CNN, trained independently, will modify their convolutional layers in different ways.
- We therefore need to develop a technique that allows for sharing convolutional layers between the two networks, rather than learning two separate networks.

We discuss three ways for training networks with features shared:
1. Alternating training
    - We first train RPN, and use the proposals to train Fast R-CNN.
    - The network tuned by Fast R-CNN is then used to initialize RPN, and this process is iterated.
    - This is the solution that is used in all experiments in this paper.
2. Approximate joint training
    - RPN and Fast R-CNN networks are merged into one network during training.
    - This solution is easy to implement. But this solution ignores the derivative w.r.t. the proposal boxes’ coordinates that are also network responses, so is approximate.
    - This solver produces close results, yet reduces the training time by about 25-50% comparing with alternating training.
    - This solver is included in our released Python code.
3. Non-approximate joint training
    - Beyond the scope of this paper.

### Implementation Details
- We train and test both region proposal and object detection networks on **images of a single scale**.
    - We re-scale the images such that their shorter side is s = 600 pixels.
- On the re-scaled images, the total stride for both ZF and VGG nets on the last convolutional layer is 16 pixels.
- For anchors, we use:
    - **3 scales** with box areas of 1282 , 2562 , and 5122 pixels
    - **3 aspect ratios** of 1:1, 1:2, and 2:1
- The anchor boxes that cross image boundaries need to be handled with care.
- Some RPN proposals highly overlap with each other. 
    - To reduce redundancy, we adopt non-maximum suppression (NMS) on the proposal regions based on their cls scores.
    - We fix the IoU threshold for NMS at 0.7, which leaves us about 2000 proposal regions per image.
    - After NMS, we use the top-N ranked proposal regions for detection.

## Algorithm
1. Input Image --|Re Scale Image such that shorter side $s = 600px$|--> Re-Scaled Image
2. Re-Scaled Image --|Convolution|--> Feature Map
3. Feature Map --|Slide n x n window|--> k Anchors at each window location
  - $k=3 \times 3 = 9$ is used in the paper.
    - 3 scale ($128^2$, $256^2$, $512^2$)
    - 3 Aspect ratio ($2:1$, $1:1$, $1:2$)
4. Anchors --|Region Proposal Network (RPN)|--> Object Proposals, Objectness Score
4. Object Proposals, Objectness Score --|Filteration|--> Filtered Object Proposals
5. Feature Map, Filtered Object Proposal --|Fast R-CNN|--> bbox, class label
6. bbox, class label --|Non Maximum Suppression (NMS)|--> detection bbox and class labels

