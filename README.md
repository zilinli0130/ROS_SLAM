# ROS_SLAM
The SLAM project uses RTAB-Map (Real-Time Appearance-Based Mapping) package interacting with robot in gazebo world to localize the robot position and generate the map simultaneously under ROS (Robot Operation System) framework. RTAB-Map algorithm can map the environment in 3D and enable loop enclosure to keep tracking of new unvisited and previous visited scene which improves the quality and accuracy for generating 3D map. Moreover, RTAB-Map has good speed and memory management, and it provides custom developed tools for information analysis. 


## Installation
1. Open a new terminal and build the catkin workspace:

    * `$ mkdir -p /home/workspace/catkin_ws/src`
 
    * `$ cd /home/workspace/catkin_ws/src`
 
    * `$ catkin_init_workspace`
 
  
2. Clone the project under  **/home/workspace/catkin_ws/src** directory:

    * `git clone https://github.com/tonyli0130/ROS_SLAM.git`

 
3. Make and compiler the project (**remember to source the environment variables in every new opened terminals**):
 
    * `cd /home/workspace/catkin_ws`
 
    * `catkin_make`
 
    * `source devel/setup.bash`
    
    
4. Clone the `teleop` package for controlling the robot:

    * `git clone https://github.com/ros-teleop/teleop_twist_keyboard`
 
 
5. Update and upgrade the workspace image to get the lattest features of Gazebo, open a terminal and write the following statements:

    * `$ sudo apt-get update && sudo apt-get upgrade -y`

## Usage

1. Now run the SLAM project, first launch the `world.launch` file and have the robot simulation environment ready:

    * `roslaunch my_robot world.launch`
    
    The RViz which provides a better visualization of both robot and simulation environment will open simultaneously, the fixed frame should be set to /map
    
2. Next launch the `teleop` node to control the robot:

    * `rosrun teleop_twist_keyboard teleop_twist_keyboard.py`

3. Next launch the `mapping.launch` which will do the SLAM process later:

    * `roslaunch my_robot mapping.launch`
  
 
   After launching the `world.launch` , `teleop_twist_keyboard.py` and `mappping.launch` , the SLAM process is ready. Navigate to the terminal where the `teleop` node is launched, follow the keyboard instruction and use keyboard to control the robot.
   Try to navigate the robot traversing all the rooms with different paths in order to do the loop closure. Go back to RViz and the map should be generated properly as shown below:
   
   ![2D Map](https://user-images.githubusercontent.com/60047845/89340491-74552700-d665-11ea-8663-b87153c15d93.PNG)

4. Finally use `ctrl+c` to terminate the `mapping.launch`, the `rtabmap.db` which shows visulization of 3D map will be saved after few seconds. Open the `rtabmap.db` file by using the following command:
    
    `rtabmap-databaseViewer ~/.ros/rtabmap.db`
    
    The `rtabmap-databaseViewer` graphical intrface will open shortly. Once open, we will need to add some windows to get a better view of the relevant information, so:

        * Say yes to using the database parameters
        * View -> Constraint View
        * Edit -> View 3D map
    
    The 3D map will be generated and appear after few minutes as shown below:
    
    ![3D Map](https://user-images.githubusercontent.com/60047845/89340506-7919db00-d665-11ea-81d2-ebe2f74e5b3b.PNG)
   
   
