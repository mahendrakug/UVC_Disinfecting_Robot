# UVC_Disinfecting_Robot
UVC_Disinfecting_Robot uses SLAM (ROS) with a Kinect to navigate in its environment. It is powered by ROS running on a Jetson Nano and an Arduino Mega that controls two motors with encoders.


In its current state the robot can use SLAM (RTABMap) to create a map of its surroundings (using the Kinect depth perception and converting it into a laserscan type message to detect wall and obstacles) and localize itself within the map. It plans a path multiple goals to achieve autonomous navigation with obstacle avoidance and human detection features.

## UVC_Disinfecting_Robot Characteristics
UVC_Disinfecting_Robot is a differential drive robot with the motors placed on the same axis. The base is made of clear acrylic and metal brackets with one caster wheel for support.
### Schematics


### ROS packages
* #### uvc_robot:
This package includes all the robot files that are needed to setup the robot. The package includes several launch files used to test the robot, start the mapping and begining the navigation. The launch file "urdf.launch" launches the joint and robot state publisher as well as RViz to display the model.
* #### uvc_robot_description:
This package includes the URDF file.
* #### uvc_robot_detailed_description:
This package includes the URDF description of the robot and the associated CAD files for display in RViz.
* #### Arduino Code:
The arduino subscribes to "cmd_vel" node and receives the command order from the move base node which specifies the motor speeds. It also sends back the encoder data needed for the odometry to be used in localisation through ROSSerial.

## How to use UVC_Disinfecting_Robot
### Packages installation
The software for the UVC_Disinfecting_Robot project was developped with ROS Melodic and Ubuntu 18.04. More recent versions should work as well but might require some tweaking.

#### To use Nox you will need the following packages (most of them should already be installed by default or requested when building the UVC_Disinfecting_Robot packages):
* The [navigation stack](https://wiki.ros.org/navigation),
* The freenect package (for connecting to the Kinect)
* [RViz](http://wiki.ros.org/rviz)
* [TF](http://wiki.ros.org/tf), [Joint State](http://wiki.ros.org/joint_state_publisher) and [Robot State](http://wiki.ros.org/robot_state_publisher) Publishers
* [ROSSerial package](http://wiki.ros.org/rosserial) (for connecting to the Arduino Mega)
* [rtabmap_ros](https://wiki.ros.org/rtabmap_ros).

## Running UVC_Disinfecting_Robot

In order to navigate UVC_Disinfecting_Robot you will need to start two launch files.
### 1. Connect to the jetson nano to Wi-Fi using a wifi module.
Then connect using vnc viewer on your laptop/PC and now you have access to the jetson nano from your remote pc.

### 2. Start the odometry and motor control
Use the following command to start the testing program:

`roslaunch uvc_robot driver.launch`

It will launch the serial controller node connected to the Arduino, the odometry node and the joint state publisher. If this step succeded you should see the side light of the robot going from a series of three quick blinks to a slow "breathing-like" type of blinking.

### 3. Start the mapping
In order to be able to map you have to use a launch file.

`roslaunch uvc_robot slam.launch`

It will launch the kinect node, rtabmap_ros node, telop keyboard and RViz. Using the ROS teleop keyboard to control the robot to map the environment:

### 3. Start the navigation and the human detection
Use the following command to start the main program:

`roslaunch uvc_robot uvc_robot_bringup.launch`

It will launch the map server to save the map files (map1.pgm and the yaml file), the navigation stack - (acml.launch, move_base.launch), the cmd_vel mux and RViz.

##Voila 

## Authors

* **Marwan Hesham** 
* **Omar Atef** 
* **Abdulrahman Atef** 

## License

This project is licensed under the GNU General Public License version 3

