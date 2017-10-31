# ROS Beginner Tutorials

## Overview

In this project, simple ROS publisher and subscriber were implemented in C++. The publisher and subscriber nodes were designed as explained in the ROS tutorials. The publisher node was modified to publish a custom string instead of the one given by the tutorial. The communication between nodes is done with a service that can be found in the `srv` folder.

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
git clone https://github.com/MichiMaestre/beginner_tutorials.git
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
rosrun beginner_tutorials talker
```
The terminal should output messages similar to:
`[ INFO] [1509468152.573652817]: Michi's custom string 315`

* In a third terminal:
```
cd ros_ws
source devel/setup.bash
rosrun beginner_tutorials listener
```
The terminal should output messages similar to:
`[ INFO] [1509468152.574110066]: I heard: [Michi's custom string 315]`
