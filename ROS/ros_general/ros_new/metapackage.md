# Metapackages
1. It is often convenient to group multiple packages as a single logical package.
	- This can be accomplished through ==metapackages.==
2. Metapackages are specialized Packages in ROS (and catkin).
	- They do not install files (other than package.xml)
	- They do not contain any
		- tests
		- code
		- files
		- or other items usually found in packages.
3. A metapackage is used in a similar fashion as virtual packages are used in the debian packaging world.
	- A metapackage simply references one or more related packages which are loosely grouped together.