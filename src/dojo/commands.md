# Installing packages

### Gazebo
```
sudo apt install ros-humble-gazebo-ros-pkgs
```

### colcon
```
sudo apt install python3-colcon-common-extensions
```

### Controller manager
```

```

# Ros 2 Control
- Controller manager - finds all the codes for divers and links them together. Uses plugins

- Uses command interfaces and state interfaces 
    - state interfaces are read-only
    - command interfaces are read/write. Things that we can control e.g velocity
- Hardware interfaces are managed by resource manager that knows about them using ```<ros2_control>``` on the urdf

### Installation

```
sudo apt install ros-humble-ros2-control ros-humble-ros2-controllers ros-humble-gazebo-ros2-control
```
# Running the package