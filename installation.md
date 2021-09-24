## Installation

This installation documentation helps in setting up the code base to run the software related to our paper. A sample visualization of payload estimation is as shown below:


<p align="center">

https://user-images.githubusercontent.com/6505998/134699009-4887d23b-070b-4ba5-a1ab-2b27a3f615bd.mp4

</p>

### Dependencies

Please follow the installation instructions for each of the dependencies.

- [YARP](https://github.com/robotology/yarp) - Robotics Middleware
- iDynTree - Branch: [feature/stack-of-tasks-berdy](https://github.com/ami-iit/idyntree-hde-fork/tree/feature/stack-of-tasks-berdy) - Library for whole-body human dynamics estimator
- ROS Rviz [Melodic](http://wiki.ros.org/melodic/Installation/Ubuntu) or [Noetic](http://wiki.ros.org/noetic/Installation/Ubuntu) - 3D Visualization


### Human Dynamics Estimation

The main code related to the estimation of payload and articular stress are implemented as a part of [Human Dynamics Estimation](https://github.com/robotology/human-dynamics-estimation) project in the branch [feature/SOT-Berdy-HDE](https://github.com/robotology/human-dynamics-estimation/tree/feature/SOT-Berdy-HDE).

Follow the installation instructions from the [master branch](https://github.com/robotology/human-dynamics-estimation#how-to-install) and to run the payload estimation and articular stress estimation, please refer to [How to run Dynamics Estimation](https://github.com/robotology/human-dynamics-estimation/blob/master/doc/how-to-run-dynamics-estimation.md)

### Dataset

The dataset of a human manipulating a 5 Kg payload as highlighted in the video above is available at [Dataset](./dataset).
