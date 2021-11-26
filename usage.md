### Usage Instructions

:warning: Each of the steps from 1 to 6 require a dedicated terminal

Please refer to the [Installation](./installation.md) document to setup the system to run the codebase with the [dataset](./dataset).

1. Run the ROS server:  
```bash
roscore
```

2. Run the YARP server:
```bash
yarpserver --ros --write
```

3. Open the dataset:
  a. Extract the [dataset zip file](./dataset) to an accesible location
  b. Launch yarpdataplayer   
    ```bash 
    yarpdataplayer --withExtraTimeCol 2 
    ```
  c.  File->"Open Directory" -> open the directory extracted from the [dataset zip file](./Dataset)

4. Launch the Human Dynamics Estimation:
  ```bash
  yarprobotinterface --config Human_AMTI.xml
  ```
  
5. Run the state publisher:
  ```bash
  yarprobotstatepublisher --period 0.0001 --name-prefix Human --tf-prefix /Human/ --model humanSubject02_66dof.urdf --reduced-model true --base-frame Pelvis --jointstates-topic "/Human/joint_states"
  ```
  
6. Launch RVIZ with the HDE configuration:
  ```bash
  roslaunch HDERviz HDERviz.launch
  ```
  
7. Play the dataset by pressing :arrow_forward: on yarpdataplayer

8. Remove the wrench offset through `/HumanDynamicsEstimator/rpc:i` rpc port
```bash
yarp rpc /HumanDynamicsEstimator/rpc:i
removeWrenchOffset
```

⚠️ The offset removals is to be done at the **start** of the dataset, where the human subject is in neutral npose without any load in the hand. The offset removal process removes the wrench that corresponds to the difference between the mass of the actual subject and the mass of the
subject in the model. The offset removal process results in zeroing the estimated object mass.

