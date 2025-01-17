# AVP-SLAM-PLUS
## Before we go
The original Implementation is produced by Guitao Liu, and I just fix some little missed points.

AVP-SLAM-PLUS is an implementation of AVP-SLAM and some new contributions. Performance of AVP-SLAM-PLUS could be found in video(https://www.bilibili.com/video/BV11R4y137xb/)

<p align='center'>
<img src="images/mapping1.gif"  width = 30% height = 30% " />
<img src="images/mapping2.gif" width = 30% height = 30% />
<h5 align="center">mapping</h5>
</p>

<p align='center'>
<img src="images/localization1.gif" width = 30% height = 30% />
<img src="images/localization2.gif" width = 30% height = 30% />
<h5 align="center">localization</h5>
</p>

AVP-SLAM-PLUS contain a simple implementation of [AVP-SLAM: Semantic Visual Mapping and Localization for Autonomous Vehicles in the Parking Lot `IROS 2020`](https://arxiv.org/abs/2007.01813) and some new contributions.

The new contribustions are as follows:

- Firstly,the system provide two camera style mode which are multi `RGB cameras` mode and multi `RGBD cameras` mode; 
- Secondly,the system provide two registration mode which are ICP mode and NDT mode. 
- Lastly,the system provide mapping mode and localization mode, that means you can not only do SLAM,but also do localization in a prior map.

<p align='center'>
<img src="images/avp_slam_plus_frame.PNG" width = 80% height = 80% />
<h5 align="center">AVP-SLAM-PLUS Framework</h5>
</p>
This code is simple and is a good learning material for SLAM beginners.



## 1. Prerequisites
### 1.1 **Ubuntu** and **ROS**
`Ubuntu 64-bit 18.04` `ROS Melodic` `Gazebo`

Some packages of Python (eg. rospkg) are needed if necessary.

**One helpful script to install ROS enviroment (Melodic Desktop Version)** 

```bash
wget http://fishros.com/install -O fishros && sudo bash fishros
# The fishros script is also provided in this repo
```
                  
Then
- Remember to `source ~/.bashrc` file. 
- After that, you should `roscore` to initialize the ROS core at one terminal.
- Run `rosrun gazebo_ros gazebo` to test gazebo and initialize .gazebo directory in your ~/ directory. Gazebo is a simulation tool to form a virtual environment in ROS.
                  
### 1.2 **Clone AVP-SLAM-PLUS** and **Load Gazebo Model** 

Enter your /home directory and mkdir `catkin_ws` and `catkin_ws/src`

```
    cd ~/catkin_ws/src
    git clone https://github.com/Sprinter1999/AVP-SLAM-PLUS.git
    cd AVP-SLAM-PLUS/avp_slam_plus/model/
    unzip my_ground_plane.zip -d ~/.gazebo/models/
```



## 2. Build AVP-SLAM-PLUS

```
    cd ~/catkin_ws
    catkin_make
    source ~/catkin_ws/devel/setup.bash
```


## 3. RUN Example

**Keep in mind, when you need launch one node, please source the bash file firstly.**
                  
Plus, in this implementation, `mapping` and `localization` are different periods. First you should construct a global map using instructions in `Mapping` period, then just close the `mapping` process and proceed your `localization` period based on the map constructed in `Mapping` period.  
### 3.1  **RGB Mode**

#### **save map**

if you want to save map and use the map to do localization, you should ensure your config file have be correctely set. The config file is at   **AVP-SLAM-PLUS/avp_slam_plus/config/configFile.yaml**

```
    mapSave: true
    mapSaveLocation: your map file address 
```

#### 3.1.1  **Mapping**
```
    roslaunch avp_slam_plus slamRGB.launch
```

open a new terminal, control robot move. 
```
    roslaunch robot_control robot_control.launch
```
if you firstly control robot move, you should ensure **robot_control.py** in **AVP-SLAM-PLUS/simlate_gazebo/robot_control/** to be executable. you can do this command to let **robot_control.py** to be executable.
```
    chmod +777 robot_control.py
```

#### 3.1.2  **Localization**
if you have done 3.1.1 and configure your "save map", you can do localization in the prior map.
```
    roslaunch avp_slam_plus localizationRGB.launch
```


open a new terminal, control robot move
```
    roslaunch robot_control robot_control.launch
```



### 3.2  **RGBD Mode**

#### **save map**

if you want to save map and use the map to do localization, you should ensure your config file have be correctly set. The config file is at   **AVP-SLAM-PLUS-main/avp_slam_plus/configFile.yaml**
```
    mapSave: true
    mapSaveLocation: your map file address 
```


#### 3.2.1  **Mapping**
```
    roslaunch avp_slam_plus slamRGBD.launch
```

open a new terminal, control robot move
```
    roslaunch robot_control robot_control.launch
```


#### 3.2.2  **Localization**
if you have do 3.2.1 and "save map", you can do localization in the prior map.

```
    roslaunch avp_slam_plus localizationRGBD.launch
```

open a new terminal, control robot move
```
    roslaunch robot_control robot_control.launch
```



## 4.Acknowledgements

Thanks for AVP_SLAM (Tong Qin, Tongqing Chen, Yilun Chen, and Qing Su: Semantic Visual Mapping and Localization for Autonomous Vehicles in the Parking Lot),

Thanks for TurtleZhong (https://github.com/TurtleZhong/AVP-SLAM-SIM), whose simulated environment help me a lot.

Thanks for huchunxu (https://github.com/huchunxu/ros_exploring), whose simulated robot model help me a lot.

Thanks for Guitao Liu for one nice re-implementation of AVP-SLAM.
