# R.O.O.K
ROOK DROID'S workspace for [robotics dojo 2024](https://roboticsdojo.github.io/) competition. The dojo package is the main package , the articubot_one package is for reference and for any more info on how to work with this ros workspace refer to [Articulated Robotics Tutorial](https://articulatedrobotics.xyz/tutorials) , the sllidar_ros2 is for the lidar and the diffdrive_arduino is for hardware interface .


> 📝 **Note**: FOR PROPER OPERATION IN THE PI CHECKOUT TO THE `pi` BRANCH

## Packages used

### Official packages
- Gazebo
- Rviz
- Colcon
- Teleop_twist
- Twist_mux
- Nav2
- Slam Tool box
- Ros2 Control

Chekout `README_dojo.md` on installation instructions

### Github sourced packages

- **SLLidar ROS2**
  - Repository: [Slamtec/sllidar_ros2](https://github.com/Slamtec/sllidar_ros2.git)

- **Diffdrive Arduino**
  - Repository(humble branch): [joshnewans//diffdrive_arduino](https://github.com/joshnewans/diffdrive_arduino.git)
  - This node is used together with an arduino running [ros_arduino_bridge](https://github.com/joshnewans/ros_arduino_bridge.git)



### Package used for reference

- **Articubot One**
  - Repository: [joshnewans/articubot_one](https://github.com/joshnewans/articubot_one.git)
  - Based on tutorial: [Articulated Robotics Tutorial](https://articulatedrobotics.xyz/tutorials)

### Customized github package

- **Dojo**
  - Repository: [ru3ll/dojo](https://github.com/ru3ll/dojo.git)


### Additional Instructions
 For rplidar the package used is [Slamtec/sllidar_ros2](https://github.com/Slamtec/sllidar_ros2.git) and not the one used in the [Articulated Robotics Tutorial](https://articulatedrobotics.xyz/tutorials) tutorial








## IMPORTANT COMMANDS WHEN ROBOT IS FULLY RUNNING / FOR ROBOT TO FULLY RUN
> 📝 **Note**: FOR PROPER OPERATION IN THE PI CHECKOUT TO THE `pi` BRANCH
### ON BOT IN SAME NETWORK RUNNING pi BRANCH WORKSPACE

Command for robot launch file

```bash
ros2 launch dojo launch_robot.launch.py
```

sllidar_ros2 running requires the read and write permissions of the serial device.
You can manually modify it with the following command:

```bash
sudo chmod 777 /dev/ttyUSB0
```

The command for RPLIDAR A1 is :

```bash
ros2 launch sllidar_ros2 sllidar_a1_launch.py
```

## ON PC IN SAME NETWORK RUNNING main BRANCH WORKSPACE

launch rviz with the environment on the folder

```
rviz2 -d ./src/dojo/rviz/default.rviz
```


launch teleop twist keyboard
```
ros2 run teleop_twist_keyboard teleop_twist_keyboard --ros-args -r /cmd_vel:=/cmd_vel_key
```

Teleop Twist with topic remap
```
ros2 run teleop_twist_keyboard teleop_twist_keyboard --ros-args -r /cmd_vel:=/diff_cont/cmd_vel_unstamped
```

Launch SLAM for navigation
```
ros2 launch slam_toolbox online_async_launch.py slam_params_file:=./src/dojo/config/mapper_params_online_async.yaml use_sim_time:=true
```

Launch Nav2
```
ros2 launch nav2_bringup navigation_launch.py use_sim_time:=true
```

Running nav2
```
ros2 run nav2_map_server map_server --ros-args -p yaml_filename:=my_map_save.yaml -p use_sim_time:=true
```

