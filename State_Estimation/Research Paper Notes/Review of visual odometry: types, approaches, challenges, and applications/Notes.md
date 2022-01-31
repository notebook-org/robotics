## Introduction
> Vision-based navigation of mobile robots is one of the main goals of computer vision and robotics research

**Ego Motion:** 3D motion of a camera within an environment.

**Visual Odometry:** The process of estimating ego motion of agent by using only the input from camera attached to it is called visual odometry.
    - Provides an incremental online estimation of the vehicle position by analyzing the image sequences captured by a camera.
    - Pros:
        - High localization accuracy
        - Inexpencive Solution
    - Cons:
        - High localization accuracy
        - Inexpencive Solution

Visual Oodometry can be integrated with Inertial Sensors to maximum accuracy.

- Monocular vision systems suffer from scale uncertainty.
    -  If the surface is uneven, the image scale will fluctuate, and the image scaling factor will be difficult to estimate.

Most VO methods that have been proposed in existing literature use either stereo or monocular cameras and can be roughly classified as stereo or monocular VO systems.

Stereo VO can be degraded to the monocular case when the stereo baseline is much smaller than the distances to the scene from the camera.

## Approaches
1. Feature-based approach
    - Steps:
        1. Extracting Image Features
        2. Associate features between subsequent frames.
        3. Estimating the Motion.
2. Appearance-based approach
3. hybrid of feature and appearance based approaches
