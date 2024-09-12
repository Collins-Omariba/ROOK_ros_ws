## this is the branch that should run on the pi


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

Chekout `README.md` inside dojo package for installation instructions

### Github sourced packages

- **SLLidar ROS2**
  - Repository: [Slamtec/sllidar_ros2](https://github.com/Slamtec/sllidar_ros2.git)

- **Diffdrive Arduino**
  - Repository: [ru3ll/diffdrive_arduino](https://github.com/ru3ll/diffdrive_arduino.git)
  - This node is used together with an arduino running [ros_arduino_bridge](https://github.com/joshnewans/ros_arduino_bridge.git)

- **Serial**
  - Repository: [joshnewans/serial](https://github.com/joshnewans/serial.git)

### Customized github package

- **Dojo**
  - Repository: [ru3ll/dojo](https://github.com/ru3ll/dojo.git)



## IMPORTANT COMMANDS WHEN ROBOT IS FULLY RUNNING / FOR ROBOT TO FULLY RUN

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
ros2 launch sllidar_ros2 view_sllidar_a1_launch.py
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

