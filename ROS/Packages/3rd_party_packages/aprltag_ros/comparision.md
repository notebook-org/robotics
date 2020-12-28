### Aruco (as implemented in OpenCV)
1. pros
	- Easy to set up (with readily available aruco marker generator, opencv & ros implementation, etc.) fewer false detection (with default parameters)
2. cons
	- Newer versions of aruco is GPL licensed, hence opencv is stuck on an old implementation of aruco when it was still BSD.
	- More susceptible to rotational ambiguity at medium to long ranges
	- More tuning parameters
	- More computationally intensive

###AprilTag (as implemented in apriltag_ros)
1. pros
	- BSD license
	- Fewer tuning parameters
	- Works fairly well even at long range
	- Used by NASA
	- More flexible marker design (e.g. markers not necessarily square)
	- Less computationally intensive
2. cons
	- less straight forward to setup (no opencv implementation AFAIK, only ros implementation, slightly more steps to obtain markers)
	- more false detection (with default parameters)