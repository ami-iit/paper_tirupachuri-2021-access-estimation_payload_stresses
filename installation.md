## Installation

This installation documentation helps in setting up the code base to run the software related to our paper. A sample visualization of payload estimation is as shown below:


<p align="center">

https://user-images.githubusercontent.com/6505998/134699009-4887d23b-070b-4ba5-a1ab-2b27a3f615bd.mp4

</p>

### System

⚠️ The code has been tested on Ubuntu 18.04.6 LTS (Bionic Beaver)

### Dependencies

Please follow the installation instructions for each of the dependencies.

- [Savitzky Golay](https://github.com/arntanguy/gram_savitzky_golay#installation) Filtering
- ROS Rviz [Melodic](http://wiki.ros.org/melodic/Installation/Ubuntu) or [Noetic](http://wiki.ros.org/noetic/Installation/Ubuntu) - 3D Visualization

### Robotology Codebase Components

The following are the main components that are required to run the code base for the paper.

- [YARP](https://github.com/robotology/yarp) - Robotics Middleware
- iDynTree - Branch: [feature/stack-of-tasks-berdy](https://github.com/ami-iit/idyntree-hde-fork/tree/feature/stack-of-tasks-berdy) - Library for whole-body human dynamics estimator
- [Human Dynamics Estimation](https://github.com/robotology/human-dynamics-estimation) project in the branch [feature/SOT-Berdy-HDE](https://github.com/robotology/human-dynamics-estimation/tree/feature/SOT-Berdy-HDE)

#### Robotology Installation

Installing the components of Robotology of the code associated with the paper seperately can be tricky. [Robotology-superbuild](https://github.com/robotology/robotology-superbuild) offers a convenient way to setup the required infrastructure, using [robotology project tags](https://github.com/robotology/robotology-superbuild/blob/master/doc/change-project-tags.md). The required version of the code are updated in [aeps.yaml](./aeps.yaml). Please follow the instructions below to setup robotology components.

```
git clone https://github.com/dic-iit/tirupachuri-2021-access-estimation_payload_stresses
export AEPS_ROOT=`pwd`/tirupachuri-2021-access-estimation_payload_stresses
git clone https://github.com/robotology/robotology-superbuild
cd robotology-superbuild
git checkout -b v2021.08
cmake -DROBOTOLOGY_PROJECT_TAGS:STRING=Custom -DROBOTOLOGY_ENABLE_HUMAN_DYNAMICS=True -DROBOTOLOGY_PROJECT_TAGS_CUSTOM_FILE=${AEPS_ROOT}/aeps.yaml ..
```

⚠️ Do not build `robotology-superbuild` without the `ROBOTOLOGY_PROJECT_TAGS_CUSTOM_FILE` option pointed to [aeps.yaml](./aeps.yaml) file. Check the description at the end of [robotology project tags](https://github.com/robotology/robotology-superbuild/blob/master/doc/change-project-tags.md) for further information.

### Dataset

The dataset of a human manipulating a 5 Kg payload as highlighted in the video **above** is available at [Dataset](./dataset). This dataset is acquired with Xsens system for whole-body motion tracking, and AMTI force/torque ground fixed platform for ground reaction wrench at the feet. The logged data is in `wearable data` format that is achieved through [wearable library](https://github.com/robotology/wearables). Please refer to the [paper](https://ieeexplore.ieee.org/abstract/document/9526592) for more details on how the data is handled.

#### Playback

The dataset can be played back using [yarpdataplayer](https://www.yarp.it/latest/yarpdataplayer.html) tool

:warning: The [dataset](./dataset) contains two different time stamps, each from the machine from where the data originated, and the machine from where the data logging is done. So, for the dataset playback `yarpdataplayer` needs to be run with the argument `--withExtraTimeCol 2`

```
yarpdataplayer --withExtraTimeCol 2
```

### Configuration File

Please use the configuration file [Human_AMTI](https://github.com/robotology/human-dynamics-estimation/blob/feature/SOT-Berdy-HDE/conf/xml/Human_AMTI.xml) to run the payload and articular stress estimation. This configuration file can be launched as:

```
yarprobotinterface --config Human_AMTI.xml
```
