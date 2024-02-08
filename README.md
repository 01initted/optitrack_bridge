# optitrack_bridge

This package converts Optitrack rigidBody message to ROS1 pose/odometry/tf message.

Tested in 
- Ubuntu 20.04, ROS Noetic 

1.Prerequisite
------
This code is for below environment.
- C++14
- Motive 2.2 or 2.3
- NatNet 3.1

2.Installation
------
    cd ~/catkin_ws/src

    git clone https://github.com/01initted/optitrack_bridge.git

    cd .. && catkin_make

It assumes that your work space is in `~/catkin_ws/src`

3.Usage
------
    source devel/setup.bash
    roslaunch optitrack_bridge optitrack.launch

4.Parameters
-----
You can change the parameter in the launch file.
In the robotics env, I suggests to use publish unlabeled marker pose array.(And make your own pose estimation algo.)

**`publish_unlabeled_marker_pose_array`: If true, publish unlabeled markers as geometry::poseArray**

`frame_id`: Set frame id of message.

`message_type`: Ros message type.

+ pose - It returns the object's pose as geometry::poseStamped message.
+ odometry - It returns object's pose+twist(velocity) as nav_msgs::odometry message. The twist(velocity) of the object is computed by linear Kalman filter. (Error covariance is not supported yet.)
+ tf - It returns the object's pose as tf message.

`show_latency`: Print latency on the screen.

`publish_labeled_marker_pose_array`: If true, publish pose of object's markers as geometry::poseArray 


(If labeled or unlabeled markers are not published, check Motive -> Streaming Pane -> Labeled or Unlabeld Markers)

**5.Package**
---
Extracting the unlabled markers center position, through the ros package on local computer.
cd ~/catkin_ws/src/
catkin_create_pkg test std_msgs geometry_msgs rospy roscpp
