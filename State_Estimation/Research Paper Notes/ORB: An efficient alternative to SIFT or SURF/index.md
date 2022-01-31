# ORB: An efficient alternative to SIFT or SURF

**ORB:** A very fast binary descriptor based on BRIEF, which is rotation invarient and resistant to noise.

## Introduction
- Our proposed feature builds on the well-known FAST keypoint detector and the receintly-developed BRIEF descriptor.
    - **ORB: Oriented FAST and Rotated BRIEF**

## oFast: FAST Keypoint Orientation
- Widely used because of there computational properties.
- However, FAST feature do not have an orientation component.

### FAST Detector
- FAST takes one parameter, the intensity threshold between the center pixel and those in a circular ring about the center.
- We use FAST-9 (circle radius of 9), which has good performance.
- FAST does not produce a measure of cornerness, and we have found that it has large response along edges.
    - We employ a Harris corner measure to order the FAST keypoints.
    - For a target number N of keypoints, we first set the threshold low enough to get more that N keypoints, then order them according to the Harris measure, and pick the top N points.
- Fast dies not produce multi-scale features.
    - We employ a scale pyramid of the image, and produce FAST features at each level in the pyramid.

### Orientation by Intensity Centroid
> The intensity centroid assumes that a corner's intensity is offset from its center, and this vector may be used to impute an orientation.

Moment of patch is
$$m_{pq} = \sum_{x,y}x^py^qI(x,y))$$
and with these moments we may find the centroid:
$$C = (\frac{m_{10}}{m_{00}}, \frac{m_{01}}{m_{00}})$$

The orientation of the patch then simply is:
$$\theta = atan2(m_{01}, m_{10})$$

To improve the rotation invariance of this measure we make sure that momentum are computed with x and y remaining within a circular region of radius r (empirically chosen).
