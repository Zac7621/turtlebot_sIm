1. Instructions to launch the Turtlebot simulation

You need Ros melodic to run this simulaion, if you don't, read this to install (http://wiki.ros.org/melodic/Installation)

You will also need the gmapping and dwa_local_planner packages, if not installed during the ros installation, get it from your package manager or clone in your catkin/src repo from the source repositories.


Once installed properly, clone this git into your catkin repo, and execute catkin make to coompile all necessary nodes properly.
Then, execute: source devel/setup.bash (Or put it in your .bashrc file)

You are now ready to launch the simulation, to do so execute in a command line terminal:

roslaunch turtlebot3_gazebo turtlebot3_world_teleop.launch

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

(End of Question 1 3h of work)


