ROS package for using Robai's Cyton Gamma 300 robotic arm with ROS based on Andras's Fekete work.

 Using the Power Supply for the Cyton Gamma 300:

   1. Connect the negative and positive wires of the power cable to the terminals on the power supply.
   2. Plug in and power on the power supply.
   3. Adjust the coarse and fine voltage knobs until the power supply is 12.0 volts.
   4. Use a multimeter to confirm the voltage is 12.0 volts:
       a. Plug the black cable into the COM port and the red cable to the V? port.
       b. Switch the multimeter to the 20V DC selection.
       c. Touch the red cable to the positive terminal and the black cable to the negative terminal on the power supply.
       d. Read the multimeter and adjust the fine voltage on the power supply until it reads 12.0 volts.
   5. Read the max amperage with the multimeter:
       a. Plug the black cable into the COM port and the red cable to the 20A port.
       b. Switch the mutlimeter to the 20m DC selection.
       c. Touch the red and black cables to the power supply terminals as before (there may be a small spark, this is fine and safe).
       d. Adjust the coarse and fine amperage knobs on the power supply until the multimeter reads 4.0A
   6. You may now use the power supply on the arm.

   Running the ROS software on the Cyton Gamma 300:

   1. Install and configure a ROS Indigo:
       http://wiki.ros.org/ROS/Tutorials/InstallingandConfiguringROSEnvironment
   2. Install the moveit_plugins and industrial_core:
       sudo apt-get install ros-indigo-industrial-core
       sudo apt-get install ros-indigo-moveit-plugins
   3. Clone the workspace:
       git clone git@bitbucket.org:AndLydakis/cyton_gamma_300_ros.git
   4. Download the dependencies for the repository as well:
       a. The dynamixel controllers, drivers, and message descriptions:
           git clone https://github.com/arebgun/dynamixel_motor.git
       b. The ROS-Industrial core meta-package:
           git clone https://github.com/ros-industrial/industrial_core.git
   5. Compile all the packages (you may optionally use the Debug build type):
       catkin_make -DCMAKE_BUILD_TYPE=Debug

   Launching the arm softawre:
   
   On every terminal cd to cyton_gamma_300_ROS/ROS_ws/ and source /devel/setup.bash or add it to your ~/.bashrc 
   1.  Terminal 1 : roslaunch cyton_controllers controller_manager.launch.
   2.  You should get an output similar to the following:
![term1](gamma_images/ros_arm1.png)
   3.  Terminal 2 : roslaunch cyton_controllers start_controller.launch
   4.  On terminal 2 you should get the following output :
![term1](gamma_images/ros_arm2.png)
   5.  On terminal 1 you should get the following output :
![term1](gamma_images/ros_arm3.png)
   6.  Terminal 3 : roslaunch cyton_controllers gripper_manager.launch
   7.  You should get an output similar to the following:
![term1](gamma_images/ros_arm4.png)
   8.  Terminal 4 : roslaunch cyton_controllers gripper_controller.launch
   9.  On terminal 3 you should get the following output :
![term1](gamma_images/ros_arm5.png)
   10. On terminal 4 you should get the following output :
![term1](gamma_images/ros_arm6.png)
   11. Terminal 5 : roslaunch cyton_gamma_300_andreas_configuration moveit_planning_execution.launch
![term1](gamma_images/ros_arm7.png)
   12. From that point, connect to the database in the MoveIt panel and select a planning algorithm.
   13. Manipulate the axes in Rviz to get the position you need, and from the planning tab select "Plan & Execute". You can save states and load them as long as you use the same database

   If you want to use the Kinect with the as well:
   1.  Terminal 1: roslaunch openni2_launch openni2.launch
   2.  Terminal 2: roslaunch eyes track_kinect.launch
   3.  Terminal 3: Depending on where the camera is setup in regards to the arm, set up a static transform publisher
   3.  In Rviz set the Camera visualisation to the appropriate topic, and experiment with the markers.
