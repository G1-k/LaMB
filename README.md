[//]: # (Image Reference)

[image1]: ./images/lamb.jpg


# LaMB <br> [![CC BY-NC-SA 4.0][cc-by-nc-sa-shield]][cc-by-nc-sa] [![CC BY-NC-SA 4.0][cc-by-nc-sa-image]][cc-by-nc-sa]


## Localization and Mapping Bot a.k.a LaMB

![alt_text][image1]

LaMB is a differential drive robot which uses SLAM with RPLidar to navigate in its environment. It uses Jetson Nano as a companion computer for path planning and obstacle avoidance

### Getting Started

1. Give a star to this repo (at the top) 

2. Install Pre-requisite
```
sudo apt-get install ros-melodic-gmapping ros-melodic-teleop-twist-keyboard ros-melodic-map-server ros-melodic-amcl ros-melodic-move-base
```

3. Clone the repository

- `cd catkin_ws/src`
- `git clone https://github.com/G1-k/LaMB.git`
- `git clone https://github.com/NickL77/RPLidar_Hector_SLAM.git`	

3. Build the workspace
```
cd ..
catkin build
```
### Generate Map using GMapping

#### Launch Respective Nodes

1. Launch Hardware related Nodes:
```
roslaunch lamb hardware.launch
```
OR Launch these individually(Optional):

	* Arduino Bridge Node
	
	roslaunch ros_arduino_python arduino.launch
	

	* RPLidar Node
	
 	roslaunch rplidar_ros rplidar.launch
 	

2. Gmapping node
``` 
roslaunch lamb gmapping.launch
```

3. Visualization
```
cd catkin_ws/src/LaMB/rviz 
rviz -d map.rviz
```
4. Teleop Node
```
 rosrun teleop_twist_keyboard teleop_twist_keyboard.py 
```
Using Arrow keys drive the robot around to generate map.

5. After completing map, Save it 
```
 rosrun map_server map_saver -f ~ ~/catkin_ws/src/lamb/maps/name_of_map
```


### Navigation

1. Launch Navigation:
```
roslaunch lamb navigation.launch savedmap:='name-of-map'
``` 
OR Launch these individually (Optional)

	* AMCL Node
	
 	roslaunch lamb amcl.launch map:='name-of-map
	

	* Move base Node
	
	roslaunch lamb move_base.launch
	

2. Visualization
```
 cd catkin_ws/src/LaMB/rviz
 rviz -d navigate.rviz
```
3. Go to goal
* Set initial pose using 2D pose estimate in Rviz.
* Optional : Use teleop until pose estimates(red_particles) are accurate.
* Set goal postion and orientation using 2D Nav goal 

### Don't forget to give a star (at top of the repo) 

[cc-by-nc-sa]: http://creativecommons.org/licenses/by-nc-sa/4.0/
[cc-by-nc-sa-image]: https://licensebuttons.net/l/by-nc-sa/4.0/88x31.png
[cc-by-nc-sa-shield]: https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg
This work/project is licensed under a [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International Public License][cc-by-nc-sa]. 

### Contributing 

1. Fork it!
2. Create your feature branch : ` git checkout -b my-new-feature`
3. Commit your changes: ` git commit -am 'Add some feature'`
4. Push to the branch: `git push origin my-new-feature`
5. Submit a pull request
