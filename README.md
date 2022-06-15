1. Instructions to launch the Turtlebot simulation

You need Ros melodic to run this simulaion, if you don't, read this to install (http://wiki.ros.org/melodic/Installation)

You will also need the gmapping and dwa_local_planner packages, if not installed during the ros installation, get it from your package manager or clone in your catkin/src repo from the source repositories.


Once installed properly, clone this git into your catkin repo, and execute catkin make to coompile all necessary nodes properly.
Then, execute: source devel/setup.bash (Or put it in your .bashrc file)

You are now ready to launch the simulation, to do so execute in a command line terminal:

roslaunch turtlebot3_gazebo turtlebot3_world_mux.launch

Gazebo should launch the robot simulation and the world we selected.
Rviz should launch as well allowing you to see all the topcis from the robot.
Finally you will be able to move the robot from your keyboard using the following commands :

---------------------------
Moving around:
        z
   q    s    d
        x
        
z/x : increase/decrease linear velocity (Burger : ~ 0.22)
q/d : increase/decrease angular velocity (Burger : ~ 2.84)

space key, s : force stop

2. Map the world to prepare for autonomous navigation through SLAM.

If you want to perform autonomous navigation, you will first need to map the world the robot is in.

To do so execute : 

roslaunch turtlebot_gazebo turtlebot_world_mapping.launch

This will launch the same simulaion as earlier but will bring you the map node in rviz.

With this navigate in the evronment with the same commands as before until the map in rviz matches the world you put the robot in.

Then save the map with :

rosrun map_server map_saver 

inside the repository you want to save the map.

3. Run autonomous navigation

In order to run this simulation, execute

roslaunch turtlebot3_gazebo turtlebot3_world_navigation.launch

and in an other terminal run :

rosrun turtlebot3_teleop turtlebot3_teleop_key

in Rviz select the 2D pose estimate and point it at the position of the robot in the map,and drag towards its direction.

Then teleoperate the robot back and forth to allow him to estimate its position correctly. When this is done, close the teleoperation node.

To perform autonomous navigation click the 2D nav goal and point your mouse where you want the robot to go, then drag towards the direction you want the robot to stop in.

Enjoy the ride!!

(End of Question 1 3h of work with testing and documentation)


The multiplexer node has been implemented in the launchfiles for easier use.

The used node is the mux node from the topic_tools package.

You can choose between cmd_local and cmd_web to send commands to the robot.

To switch between the two use

rosrun topic_tools mux_select mux_cmdvel [cmd_local or cmd_web]

The node will select cmd_local by default.

End of question 2 30 min with testing and documentation.


Mqtt "Remote" Teleoperation

To make this feature I started from the teleoperation ros node that exists whithin the turtlebot package.

I reused the function to gather data from the keyboard and created a dict to create the commands for the robot, and dumped this dict into a Json message to send it through the mqtt broker.

In the ros node, the message is turned back into a dict from the mqtt callback, and published in the cmd_web topic for the robot.

To run this simulation, run the mulitplexer simulation from question 1, then run from your home repository

./catkin_ws/src/turtlebot3_simulations/turtlebot3_teleop/nodes/mqtt_teleop_key for the mqtt teleop program

and 

./catkin_ws/src/turtlebot3_simulations/turtlebot3_teleop/nodes/ros_mqtt_teleop_key for the ros node.

End of question 3 (4h of work documentation and tests included)
