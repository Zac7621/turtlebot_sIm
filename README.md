1. Instructions to launch the Turtlebot simulation

You need Ros melodic to run this simulaion, if you don't, read this to install (http://wiki.ros.org/melodic/Installation)


Once installed properly, clone this git into your catkin repo, and execute catkin make to coompile all necessary nodes properly.
Then, execute: source devel/setup.bash (Or put it in your .bashrc file)

You arz now ready to launch the simulation, to do so execute in a command line terminal:

roslaunch turtlebot_gazebo turtlebot_world_teleop.launch

Gazebo should launch the robot simulation and the world we selceted.
Rviz should launch as well allowing you to see all the topcis from the robot.
Fnially you will be able to move the robot from your keyboard using the following commands :

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

With this navigate in the evronment wirth the same commands as before until the map in rviz matches the world you put the robot in.

Then save the map with :

rosrun map_server map_saver 

inside the repository you want to save the map.

