# Spatial Pyramid Pooling in Deep Convolutional Networks for Visual Recognition

**Spatial Pyramid Pooling:** Generates fixed-length representation regardless of image size/scale.

(H x W x k) --|Spatial Pyramid Pooling|--> (1 x k) + (4 x k) + (16 x k)
Feature Map -----------------------------> Max pooling over pyramid of spacial bins.

## Spatial Pyramid Pooling for Object detection
* (H x W x C) Image --|Convolutions|--> (H x W x k) Feature Map
* For every region proposal in feature map:
  * (h x w x k) --|SPP|--> f (fixed size feature vector) 
  * f --|FC|--> bbox && Class label
