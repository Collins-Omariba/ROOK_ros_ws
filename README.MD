# R.O.O.K and ECHO

Welcome to **ROOK DROID and ECHO** teams workspace for the [Robotics Dojo 2024](https://roboticsdojo.github.io/) competition.
You can checkout the Technical design Paper for this project [here](https://drive.google.com/file/d/1gMHdSiueBZalDLPn9yPsRakybKB0Rzj9/view?usp=sharing)

This workspace contains several key packages and resources to operate and simulate the robot.

- The **dojo** package is the main package.
- The **articubot_one** package is used as a reference.
- For detailed information on how to work with this ROS2 workspace, refer to the [Articulated Robotics Tutorial](https://articulatedrobotics.xyz/tutorials).
- **sllidar_ros2** handles the lidar functionality.
- **diffdrive_arduino** provides the hardware interface.

> 📝 **Note**: For proper operation on the Raspberry Pi, switch to the `pi` branch. If you encounter issues with the main branch on your PC or development machine, try using the `demo` branch.

---

## Packages Used

### Official ROS2 Packages

- **Gazebo** (robot simulation)
- **Rviz** (visualization)
- **Colcon** (build system)
- **teleop_twist_keyboard** (teleoperation)
- **twist_mux** (command multiplexing)
- **Nav2** (navigation)
- **SLAM Toolbox** (simultaneous localization and mapping)
- **ros2_control** (control)

> For installation instructions, see `README_dojo.md`.

---

### GitHub-Sourced Packages

- **SLLidar ROS2**
  - Repository: [Slamtec/sllidar_ros2](https://github.com/Slamtec/sllidar_ros2.git)


- **DiffDrive Arduino** (Humble Branch)
  - Repository: [joshnewans/diffdrive_arduino](https://github.com/joshnewans/diffdrive_arduino.git)
  - Utilizes an Arduino Uno running [ros_arduino_bridge](https://github.com/joshnewans/ros_arduino_bridge.git). You can checkout the `ros_arduino_bridge` branch for the code used in our implementation.
  
### Reference Package

- **Articubot One**
  - Repository: [joshnewans/articubot_one](https://github.com/joshnewans/articubot_one.git)
  - Based on the [Articulated Robotics Tutorial](https://articulatedrobotics.xyz/tutorials).

### Customized GitHub Package

- **Dojo**
  - Repository: [ru3ll/dojo](https://github.com/ru3ll/dojo.git)

> **Note**: For the RPLIDAR, the used package is [SLLidar ROS2](https://github.com/Slamtec/sllidar_ros2.git), not the one used in the Articulated Robotics Tutorial.

---

## Running the Robot or Simulation

> 📝 **Note**: To run the robot on Raspberry Pi, switch to the `pi` branch.

### On the Robot (Raspberry Pi) — `pi` Branch

If you only want to run the simulation, skip the robot commands and execute the following on your PC workspace (using the `main` branch):

```bash
ros2 launch dojo launch_sim.launch.py world:=./src/dojo/worlds/dojo2024
```

For real-world robot operation, use the following commands:

1. **Launch the robot:**

    ```bash
    ros2 launch dojo launch_robot.launch.py
    ```

2. **Give read/write permissions to the serial device for sllidar_ros2:**

    ```bash
    sudo chmod 777 /dev/ttyUSB0
    ```

3. **Launch RPLIDAR A1:**

    ```bash
    ros2 launch sllidar_ros2 sllidar_a1_launch.py
    ```

---

### On the PC — `main` Branch

1. **Launch twist_mux for velocity commands:**

    ```bash
    ros2 run twist_mux twist_mux --ros-args --params-file ./src/dojo/config/twist_mux.yaml -r cmd_vel_out:=diff_cont/cmd_vel_unstamped
    ```

2. **Launch Rviz for visualization:**

    ```bash
    rviz2 -d ./src/dojo/rviz/default.rviz
    ```

3. **Launch teleop for keyboard control *OR* use joystick:**


    ```bash
    ros2 run teleop_twist_keyboard teleop_twist_keyboard --ros-args -r /cmd_vel:=/cmd_vel_key
    ```


    ```bash
    ros2 launch dojo joystick.launch.py
    ```
4. **Launch SLAM for simultaneous localization and mapping:**

    ```bash
    ros2 launch slam_toolbox online_async_launch.py slam_params_file:=./src/dojo/config/mapper_params_online_async.yaml use_sim_time:=false
    ```

---

## Navigating the Robot

After completing the above steps, choose one of the following options based on your setup and replace my_map_save with the name of your map saved in the workspace folder:

### Option 1: Launch Nav2

```bash
ros2 launch nav2_bringup navigation_launch.py use_sim_time:=false
```

### Option 2: Localization with AMCL

- **Using dojo's localization launch:**

    ```bash
    ros2 launch dojo localization_launch.py map:=./my_map_save.yaml use_sim_time:=false
    ```

- **Or using Nav2's localization launch:**

    ```bash
    ros2 launch nav2_bringup localization_launch.py map:=./my_map_save.yaml use_sim_time:=false
    ```

---

- **Using dojo's navization launch:**

    ```bash
    ros2 launch dojo navigation_launch.py use_sim_time:=false map_subscribe_transient_local:=true params_file:=./src/dojo/config/nav2_params.yaml
    ```

- **Or using Nav2's navigation launch:**

    ```bash
    ros2 launch nav2_bringup navigation_launch.py use_sim_time:=false map_subscribe_transient_local:=true params_file:=./src/dojo/config/nav2_params.yaml
    ```


> For more details, refer to `README_dojo.md`.

--- 

