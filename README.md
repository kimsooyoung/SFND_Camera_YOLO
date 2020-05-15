# Sensor Fusion Self-Driving Car Course - Lidar to Camera

This project implement transformation between Lidar-Sensed point cloud data and Camera image plane.

### Project Status:

![issue_badge](https://img.shields.io/badge/build-Passing-green) ![issue_badge](https://img.shields.io/badge/UdacityRubric-Passing-green)

## Dependencies for Running Locally
* cmake >= 2.8
  * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1 (Linux, Mac), 3.81 (Windows)
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* OpenCV >= 4.1
  * This must be compiled from source using the `-D OPENCV_ENABLE_NONFREE=ON` cmake flag for testing the SIFT and SURF detectors.
  * The OpenCV 4.1.0 source code can be found [here](https://github.com/opencv/opencv/tree/4.1.0)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools](https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)

## Project Overview

### 1. Show Lidar points on a top view

<img width="1112" alt="show_top_view" src="https://user-images.githubusercontent.com/12381733/77241878-fe16d180-6c3b-11ea-89e6-56782ce04254.png">

#### Implementation Step

1. Change the color of the Lidar points such that X=0.0m corresponds to red while X=20.0m is shown as green.
2. Remove all Lidar points on the road surface while preserving measurements on the obstacles in the scene.

### 2. Project Lidar Points to Camera Image Plane 

<img width="1354" alt="lidar_to_camera" src="https://user-images.githubusercontent.com/12381733/77241801-d07d5880-6c3a-11ea-8167-057c322f8317.png">

 Here's few steps for doing projection from Lidar point cloud to camera image plane.

 1. Convert each 3D point into homogeneous coordinates
 2. Apply the projection equation

<img width="675" alt="공식" src="https://user-images.githubusercontent.com/12381733/77242026-a6796580-6c3d-11ea-9a94-0f8557bcfbfb.png">

 You must first know about some parameters

  - Intrinsic camera calibration Mat > `"dat/calib_velo_to_cam.txt“`
```
"calib_velo_to_cam.txt“
calib_time: 15-Mar-2012 11:37:16
R: 7.533745e-03 -9.999714e-01 -6.166020e-04 1.480249e-02 7.280733e-04 -9.998902e-01 9.998621e-01 7.523790e-03 1.480755e-02

T: -4.069766e-03 -7.631618e-02 -2.717806e-01
…
```
  - Extrinsic Mat for rotation and translation > `"dat/calib_cam_to_cam.txt“`
```
calib_time: 09-Jan-2012 13:57:47
…
R_rect_00: 9.999239e-01 9.837760e-03 -7.445048e-03 -9.869795e-03 9.999421e-01 -4.278459e-03 7.402527e-03 4.351614e-03 9.999631e-01

P_rect_00: 7.215377e+02 0.000000e+00 6.095593e+02 0.000000e+00 0.000000e+00 7.215377e+02 1.728540e+02 0.000000e+00 0.000000e+00 0.000000e+00 1.000000e+00 0.000000e+00
…
```

> Those parameters and datasets provided from KITTI sensor setup

 3. Transform points back into Euclidean coordinates and store the result.

---
 ### Reference
* [The KITTI Vision Benchmark Suite](http://www.cvlibs.net/datasets/kitti/setup.php)
* [Udacity Sensor Fusion Nanodegree](https://www.udacity.com/course/sensor-fusion-engineer-nanodegree--nd313)

