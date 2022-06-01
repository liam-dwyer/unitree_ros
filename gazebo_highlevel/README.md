# Creating a High Level Control System for GO1
## For easier joint manipulation in RVIZ, change the launch file to include a joint movement gui. <br>
In `unitree_ros/robots/go1_description/launch/go1_rviz.launch` change the following lines: <br>
```launch
    <!--<node pkg="joint_state_publisher" type="joint_state_publisher" name="joint_state_publisher">
        <param name="use_gui" value="TRUE"/>
    </node>
    -->
    <!-- ADD THE FOLLOWING LINE OF CODE TO REPLACE COMMENTED LINES OF CODE -->
    <node name="joint_state_publisher_gui" pkg="joint_state_publisher_gui" type="joint_state_publisher_gui" />
```
## To allow the robots to walk in a Gazebo environment, CHVMP must be installed
Installing champ to get gait, strafe, and teleop controls:
```bash
sudo apt install -y python-rosdep
cd catkin_ws/src
git clone --recursive https://github.com/chvmp/champ
git clone https://github.com/chvmp/champ
git clone https://github.com/chvmp/champ_teleop
cd ..
rosdep install --from-paths src --ignore-src -r -y
```

With champ installed, the unitree_ros drivers must be installed into the same workspace. 
```bash 
cd /catkin_ws/src
git clone https://github.com/chvmp/unitree_ros
```
With the unitree_ros drivers installed, now the chvmp go1 config needs to be installed to control the robot in an RVIZ or Gazebo environment. <br>
To install only the necessary drivers for the go1, manual installation or a directory copy can be used. 
```bash
cd /catkin_ws/src
git clone https://github.com/chvmp/robots.git
cp -r /robots/configs/go1_config /champ
rm -r robots
catkin_make
```
Now your Gazebo and RVIZ environments are created and the environment is made. 
## Running your Gazebo or RVIZ simulations with teleop <br>
**RVIZ simulation**<br>
```bash
roslaunch go1_config bringup.launch rviz:=true
```
```bash
roslaunch champ_teleop teleop.launch
```
Now you can control the robot using keyboard commands
**Gazebo Simulation**
```bash
roslaunch go1_config gazebo.launch
roslaunch champ_teleop teleop.launch
```
More funcionality of the Gazebo environment can be achieved using Champ commands. More information can be found on the champ site: https://github.com/chvmp/robots/tree/master/configs/go1_config <br>


Now build the worspace
```bash
cd catkin_ws
catkin_make
source catkin_ws/devel/setup.bash
```
