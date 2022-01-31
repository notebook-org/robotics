## Introduction
**Part 1:** Presents a historical review of the first 30 years of research in this field and its fundamentals. 

**Part 2:** Deal with feature matching, robustness, and applications.

> Ideal and unique VO solution for every possible working environment does not exist.
> So, optimal solution should be chosen carefully according to the specific navigation environment and the given computational resources.

## History of Visual Odometry
- **structure from motion (SFM):** The problem of recovering relative camera poses and three-dimensional (3-D) structure from a set of camera images (calibrated or noncalibrated).
    - VO is a particular case of SFM.
    - The final structure and camera poses are typically refined with an offline optimization (i.e., bundle adjustment), whose computation time grows with the number of images.
    - VO focuses on estimating the 3-D motion of the camera sequentially as a new frame arrives and in real time.

- The problem of **estimating a vehicle's egomotion** from visual input alone started in the early 1980s and was described by Moravec.
    - Most of the early research in VO was done for planetary rovers and was motivated by the NASA Mars exploration program.

- **Streo Camera:** Range + Bearing information
- **Monocular Camera:** Only Bearing information
    - The interest in monocular methods is due to the observation that stereo VO can degenerate to the monocular case when the distance to the scene is much larger than the stereo baseline.

### Monocular VO
- Since the absolute scale is unknown, the distance between the first two camera poses is usually set to one.
- As a new image arrives, the relative scale and camera pose with respect to the first two frames are determined using either the **knowledge of 3-D structure** or the **trifocal tensor**.

Related works can be divided into three categories:
1. feature-based methods: based on salient and repeatable features that are tracked over the frames.
    - [Visual odometry by Nister et.al](https://ieeexplore.ieee.org/abstract/document/1315094): First real-time, largescale VO with a single camera.
2. appearance-based methods: use the intensity information of all the pixels in the image or subregions of it.
3. hybrid methods:  combination of the previous two.

- Several VO works have been specifically designed for vehicles with motion constraints.
    - The advantage is decreased computation time and improved motion accuracy.

> VO is only concerned with the local consistency of the trajectory, whereas SLAM with the global consistency.

## Formulation of the VO Problem
An agent is moving through an environment and taking images with a rigidly attached camera system at discrete time instants k. 

The set of image taken at time k is denoted by $I_{0:n} = \{I_0, ..., I_n\}$ .

For simplicity, the camera coordinate frame is assumed to be also the agent’s coordinate frame.

Two camera position at adjacent time instance $k-1$ and $k$ are related by the rigid body transformation $T_{k, k-1} \in R^{4 \times 4}$.
$$
T_{k, k-1} =
\begin{bmatrix}
R_{k, k-1} & t_{k, k-1}\\
0 & 1
\end{bmatrix}
$$

where, $R_{k, k-1} \in SO(3)$ is the rotation matrix and $t_{k, k-1} \in R^{3 \times 1}$ the translation vector.

The set $T_{1:n} = \{T_{1,0}, ... T_{n,n-1}\}$ contains all subsequent motions.

To Simplift the notation $T_{k,k-1} \equiv T_k$.

Finally, the set of camera poses $C_{0:n} = {C_0,...,C_n}$ contains the transformations of the camerawith respect to the initial coordinate frame at $k=0$.
$$C_n = C_{n-1}T_n$$

The main task in VO is to compute the relative transformations $T_k$ from the image $I_k$ and $I_{k-1}$ and then to concatenate the transformations to recover the full trajectory $C_{0:n}$ of the camera.

- An iterative refinement over the last $m$ poses can be performed after this step to obtain a accurate estimate of the local tragectory.
    - This iterative refinement works by minimizing the sum of the squared reprojection error of the reconstructed 3D points over last m images.
    - Called **Windowed-bundle adjustement**
    - The 3D points are obtained by triangulation of image points.

VO Pipeline:
```mmd
graph LR;
  a(Image Sequence) --> b(Feature Detection);
  b --> c(Feature Matching<br>or Tracking);
  c --> d(Motion Estimation);
  d --> e(Local Optimization);
```

**Feature Matching:** Detecting features independently in all the images and then matching them based on some similarity metrics.

**Feature Tracking:** Finding feature in one image and then tracking them in the next image using a local search technique, such as correlation.


