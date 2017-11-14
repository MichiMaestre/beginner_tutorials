# ROS Beginner Tutorials- Week 11 HW Branch

## Overview

In this project, simple ROS publisher and subscriber were implemented in C++. The publisher and subscriber nodes were designed as explained in the ROS tutorials. The publisher node was modified to publish a custom string instead of the one given by the tutorial.

The communication between nodes is done with a service that can be found in the `srv` folder. The package was updated by adding the service code in the talker node so that when commanded, the published string changes by using the service.

A launch file was added to run both nodes at same time. An argument to change the publisher frequency was also added in the launch file and in the code.
The logging levels INFO, DEBUG, WARN, ERROR and FATAL have been used in the package. 

For Week 11, a transform broadcaster was added to the talker node. It will create a static transform between the _world_ parent frame a frame called _talk_. A PDF file with the transforms tree is included in the results directory.

Unit testing was also implemented with rostest. It tests if the service is being created properly by creating a service client.

Lastly, `tutorial.launch` mas modified so that it includes data recording using rosbag. It records all the topics when the talker and listener nodes are running. A sample .bag file is included in the results directory of the repository.


## Dependencies

* ROS Kinetic
* Catkin
* roscpp package
* std_msgs package
* genmsg package

## How to build

* Create a catkin workspace if it was not created previously:

```
mkdir ros_ws
cd ros_ws
mkdir src
catkin_make
```
* Clone the repository and build the package:
```
cd ros_ws
cd src
git clone -b Week11_HW https://github.com/MichiMaestre/beginner_tutorials.git
cd ..
catkin_make
```

## How to run

* In a first terminal run:

```
roscore
```
* In a second terminal:
```
cd ros_ws
source devel/setup.bash
rosrun beginner_tutorials talker frequencyvalue
```
frequencyvalue is the only argument of the node and has to be an integer value. The terminal should output messages similar to:

`[ INFO] [1509468152.573652817]: Michi's custom string 315`

* In a third terminal:
```
cd ros_ws
source devel/setup.bash
rosrun beginner_tutorials listener
```
The terminal should output messages similar to:

`[ INFO] [1509468152.574110066]: I heard: [Michi's custom string 315]`


## How to call the service

* Once both nodes are running in separate terminals as described above, check in another terminal that the service is being detected. `rosservice list` should output a few services and `/change_string` should be listed.

* Now run the following commands to call the service and change the string to be published (`stringName` is the message to be published):
```
cd ros_ws
source devel/setup.bash
rosservice call /change_string stringName
```
The talker and listener terminals should output now the new message.

## How to run using launch file

* To run the package with a launch file, first close every terminal related to this package (including `roscore`).

* Now run the following commands in the terminal:
```
cd ros_ws
source devel/setup.bash
roslaunch beginner_tutorials tutorial.launch frequency:=5
```
where `frequency` is the argument that changes the publisher frequency. The value 5 is just an example and it can be changed for whatever other integer value.

* Once the `roslaunch` command is executed, another terminal will be opened with the listener output. The first terminal outputs the talker node's output.

## Inspecting TF frames

To verify that the TF frames were correctly created, two different actions can be done:

* First run the talker node in a terminal and then run tf_echo in another terminal:

```
rosrun beginner_tutorials talker frequencyvalue
rosrun tf tf_echo world talk
```
The output should be something like:
![tf_echo](/home/michi/Pictures/week11_1.png?raw=true)

* The second option is to use rqt_tf_tree. With the talker node running in a terminal, run the next command in a another terminal:

```
rosrun rqt_tf_tree rqt_tf_tree 
```

The output should be something like:
![rqttree](/home/michi/Pictures/rqt_tree.png?raw=true)

Lastly, to generate a pdf with the frames, run:

```
rosrun tf view_frames
```
