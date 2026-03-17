# Implement-image-stitching-techniques-to-create-panoramic-images-from-multiple-overlapping-photos
This repository contains a comprehensive lab and implementation for creating panoramic images from multiple overlapping photos. It covers the transition from low-level manual feature matching to using OpenCV’s built-in Stitcher API.

# Overview
The project is divided into two main approaches:

1. Manual Pipeline: A step-by-step implementation using ORB (Oriented FAST and Rotated BRIEF) for feature detection, Brute-Force matching with Lowe’s ratio test, and RANSAC-based Homography estimation.

2. OpenCV Stitcher API: Utilizing high-level classes to handle complex tasks like bundle adjustment, exposure compensation, and multi-band blending automatically.

# Requirements
To run this lab, ensure you have the following Python libraries installed:
pip install opencv-python opencv-contrib-python numpy matplotlib

# How It Works?
1. Feature Detection & MatchingWe use the ORB algorithm to find keypoints in two images. To ensure quality, we apply Lowe's Ratio Test, which compares the distance of the best match to the second-best match. If they are too similar, the match is discarded as ambiguous.
2. Homography and RANSACOnce matches are found, we calculate a Homography Matrix ($H$). We use RANSAC (Random Sample Consensus) to ignore "outlier" matches (false positives) that would otherwise distort the transformation.
3. Warping and StitchingThe images are transformed into a shared coordinate system. A translation matrix is applied to ensure no part of the image is cut off by negative pixel coordinates, and the images are merged into a final canvas.

# Output & Comparison
Mode	           Best For...	                               Geometry Model
1. PANORAMA	     Photos taken from a fixed point (tripod)	   Spherical/Cylindrical
2. SCANS	Flat   Documents or overhead drone shots	         Affine/Planar

# Conclusion
Through this lab, we demonstrate that while a manual pipeline is essential for understanding the underlying math of computer vision—such as Homography and Coordinate Transformation—production-grade tools like the OpenCV Stitcher class are necessary for handling real-world artifacts like:

1. Exposure differences between shots.
2. Ghosting caused by moving objects.
3. Projective distortion across wide-angle fields of view.

