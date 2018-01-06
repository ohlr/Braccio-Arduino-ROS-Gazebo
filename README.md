# Braccio-Arduino-ROS-Rviz
Project on the integration of the Arduino robotic arm Braccio into ROS and Rviz.

![demo](Demo/Demo.gif)

With this Code it is possible to control the joint angles of Braccio from a GUI.


## Prerequisites:


ROS (![Kinetic Kame](http://wiki.ros.org/kinetic))
	- RViz
	- ROSserial
Ubuntu (16.04)
Arduino (Uno)
[Braccio Robot](https://store.arduino.cc/tinkerkit-braccio)



Terminal 1:
```ruby
	roscore
```

Launches Roscore, that handles communictation between all ROS nodes.

Terminal 2:
```ruby
	source devel/setup.bash
	cd src/braccio_arduino_ros_gazebo
	roslaunch braccio_arduino_ros_gazebo urdf.launch model:=urdf/braccio_arm.urdf
```

Starts the GUI and publishes angles in Radian.

Terminal 3:
```ruby
	source devel/setup.bash
	cd src/braccio_arduino_ros_gazebo
	rosrun braccio_arduino_ros_gazebo parse_and_publish
```

Converts the joint angles to degrees and reduces the message size 

Terminal 4:
```ruby
    rosrun rosserial_python serial_node.py /dev/ttyACM0
```

Starts the communication between Arduino and Pc.
Change "/dev/ttyACM0" to the port the Port of your Arduino. 
You find this Information in the Arduino IDE, ArduinoIDE>Tools>Port.

Terminal 5 (optional/Debugging):
```ruby
	rostopic echo joint_array
```

view what is published to the Arduino

```ruby
	rostopic echo joint_states
```

view what is published by the joint_state_publisher (GUI)

```ruby
	rqt_graph
```

overview about the topics and nodes

Should look similar like this:

![Alt text](Demo/rosgraph.png)