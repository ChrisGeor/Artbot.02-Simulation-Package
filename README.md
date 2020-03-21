# Artbot.02-Simulation-Package

1. Inside the artbot.02 folder that you will copy to your .gazebo/models directory path, a meshes folder
is required to be created with the .dae file of your model to be visualised in gazebo
--------------------------------------------------------------------------------------------------------------------------------
2. The cone folders must be copied to your secret models directory as well 
--------------------------------------------------------------------------------------------------------------------------------
3. Ignore the rogue model.sdf and model.config files in the repository and delete them on download 
--------------------------------------------------------------------------------------------------------------------------------
4. The artbot_motion_02 is a package that should be copied into your catkin workspace . After that you will have to compile it with "catkin_make" in order to proceed with the simulation .
--------------------------------------------------------------------------------------------------------------------------------
5. The tracks folder could be copied anywhere on your pc but upon simulation launch you should always start with the .world file you want to open (the track). For instance in this context: " rosrun gazebo_ros gazebo track3.world " . With a roscore running on the background in another terminal.
--------------------------------------------------------------------------------------------------------------------------------
6. After running the world file insert the artbot.02 model with the gazebo gui in the track and make it move using the artbot_motion_02 package like this: "roslaunch artbot_motion_02 motion.launch"
--------------------------------------------------------------------------------------------------------------------------------
7. For the gmapping proccess which is included in the artbot_motion_02 package you will have to record data into a .bag file and the use the gmapping.launch file to open a server that will execute your mapping process which is further discribed below.
/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

 *skip this if you are familiar with gmapping
 
1. Use "rosbag record -O data.bag /scan /tf" (while the simulation is running. When you wish to stop recording data to be displayed         on your map press control-c on this terminal to terminate the recording process)
---------------------------------------------------------------------------------------------------------------------------------
2. In another terminal use "rosparam set use_sim_time true" (This will do something that you dont care to find out what it is but is still required)
---------------------------------------------------------------------------------------------------------------------------------
3. Below that use "roslaunch artbot_motion_02 gmapping.launch" (This will execute the gmapping.launch file that generates the server in which the data we recorded will be played in and transformed into a live visual map)
---------------------------------------------------------------------------------------------------------------------------------
4. In another terminal use "rosbag play data.bag" (This will trigger the data playback in the server we opened in the step above)
---------------------------------------------------------------------------------------------------------------------------------
5. When the proccess is completed without closing the gmapping.launch terminal ,use "rosrun map_server map_saver" on any available terminal
---------------------------------------------------------------------------------------------------------------------------------
6. You should see results.
 
