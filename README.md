# Exercise 1.3. Point features: webcam_point_features

Detection of ORB features from online webcam imges.
In the Git  repository https://github.com/beta-robots/webcam_point_features

- Fork it
- Build the point_features example. (mkdir build & cd build & cmake .. & make)
- Play with it
- Find out information about ORB features and describe them in your words. Document your Readme.md and cite the used references

ORB comes from Oriented FAST and Rotated BRIEF, as the name indicates, it is built on FAST keypoint detector and recently-developed BRIEF descriptor. Both techniques are attractive because of their good performance and low cost.

If we focus on the detector, FAST is the method for finding keypoints in real-time systems that match visual features, for example, Parallel Tracking and Mapping. It starts by detecting FAST points in the image. FAST takes one parameter, the intensity threshold between the center pixel and those in a circular ring about the center. 
The problem is that FAST does not produce a measure of cornerness, and it has large responses along edges. To solve this problem, it is necessary to employ a Harris corner measure to order the FAST keypoints. For a target number N of keypoints, first it has to be set the threshold low enough to get more than N keypoints, then order them according to the Harris measure, and pick the top N points. FAST does not produce multi-scale features. Because of that it has to be employed a scale pyramid of the image and produce FAST features (filtered by Harris) at each level in the pyramid.
FAST does not include an orientation operator, so for doing this task it has been included a centroid technique for measuring orientation of corners. The technique of intensity centroid assumes that a corner’s intensity is offset from its center, and this vector may be used to impute an orientation giving a single dominant result.

If we focus on the descriptor, BRIEF is a bit string description of an image patch constructed from a set of binary intensity tests. Consider a smoothed image patch, p. The feature is defined as a vector of n binary tests.
The problem with BRIEF descriptor is that it is very sensitive to in-plane rotation, matching performance of BRIEF falls off sharply for in-plane rotation of more than a few degrees. To solve this problem BRIEF must be steer according to the orientation of keypoints. For any feature set of n binary tests at location (xi , yi), define the 2 × n matrix
Using the patch orientation θ and the corresponding rotation matrix Rθ, It can be construct a “steered” version of BRIEF.
To recover from the loss of variance in steered BRIEF, and to reduce correlation among the binary tests, ORB contains a a learning method for choosing a good subset of binary tests, which is called rBRIEF.

References:
http://www.willowgarage.com/sites/default/files/orb_final.pdf


- Try to detect features more sparse over all the image, by using the mask: (http://docs.opencv.org/2.4.11/modules/features2d/doc/common_interfaces_of_feature_detectors.html#featuredetector-detect)
