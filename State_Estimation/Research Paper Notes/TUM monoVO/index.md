# TUM monoVO

## References
* [Website](https://vision.in.tum.de/data/datasets/mono-dataset)
* [Github](https://github.com/tum-vision/mono_dataset_code)

- Dataset for evaluating the tracking accuracy of monocular Visual Odometry (VO) and SLAM methods.
- All sequences contain mostly exploring camera motion, starting and ending at the same position:
    - This allows to evaluate tracking accuracy via the accumulated drift from start to end, without requiring ground-truth for the full sequence.

In contrast to existing datasets, all sequences are **photometrically calibrated**.

We provide:
1. exposure times for each frame as reported by the sensor
2. the camera response function
3. the lens attenuation factors (vignetting).
