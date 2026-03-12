# TurtleBot3 Maze Navigator

A ROS 2 Humble workspace for simulating and autonomously navigating a **TurtleBot3 Waffle** through a custom hexagonal **Maze** environment using the ROS 2 navigation stack.

The project demonstrates a full robotics pipeline including **simulation, SLAM mapping and autonomous navigation** using Python APIs.

---

# Features

* **Custom Gazebo Simulation** with a hexagonal Sigma Maze environment
* **TurtleBot3 Waffle Configuration** with LiDAR and camera sensors
* **SLAM Mapping** using SLAM Toolbox for 2D LiDAR-based mapping
* **Autonomous Navigation** using the Nav2 stack
* **Programmatic Goal Control** via nav2_simple_commander Python API

---

# System Requirements

* **OS:** Ubuntu 22.04
* **ROS2:** ROS 2 Humble Hawksbill
* **Simulation:** Gazebo

---

# Dependencies Installation

## Prerequisites

Install ROS2 Humble if not already installed:

```bash
sudo apt update
sudo apt install -y ros-humble-desktop
```

Initialize rosdep:

```bash
sudo rosdep init
rosdep update
```

---

# Workspace Setup

Create a ROS2 workspace and clone the required repositories.

```bash
mkdir -p ~/turtlebot3_ws/src
cd ~/turtlebot3_ws/src
```

Clone TurtleBot3 simulation packages:

```bash
git clone -b humble https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git
```

Clone this repository:

```bash
git clone https://github.com/morshed-asif/turtlebot3_maze_navigator.git
```

---

# Build Instructions

Build the workspace:

```bash
cd ~/turtlebot3_ws
colcon build --symlink-install
```

Source the workspace:

```bash
source install/setup.bash
```

Add to `.bashrc` for automatic sourcing:

```bash
echo "source ~/turtlebot3_ws/install/setup.bash" >> ~/.bashrc
```

---

# Launch Commands

## Basic Simulation

Set the TurtleBot3 model:

```bash
export TURTLEBOT3_MODEL=waffle
```

Launch the custom maze environment:

```bash
ros2 launch turtlebot3_gazebo turtlebot3_my_maze.launch.py
```

---

# Navigation

Launch the navigation stack with the generated map:

```bash
ros2 launch turtlebot3_navigation2 navigation2.launch.py \
use_sim_time:=True \
map:=~/turtlebot3_maze_navigator/maps/sigma_maze.yaml
```

This launches:

* Nav2 planner
* Local and global costmaps
* AMCL localization
* Behavior tree navigation

---

# Autonomous Mission Script

Run the Python navigation script:

```bash
python3 ~/turtlebot3_maze_navigator/nav2_commander_api.py
```

The script sends navigation goals programmatically using the **BasicNavigator API**.

---

# Repository Structure

```
turtlebot3_maze_navigator
│
├── maps
│   ├── sigma_maze.yaml
│   └── sigma_maze.pgm
│
├── src
│   ├── launch
│   └── worlds
│
├── nav2_commander_api.py
└── README.md
```

### Package Description

| Component             | Description                                                 |
| --------------------- | ----------------------------------------------------------- |
| maps                  | Occupancy grid maps generated from SLAM and refined in GIMP |
| src                   | Custom Gazebo world files and launch configurations         |
| nav2_commander_api.py | Python navigation controller using Nav2 API                 |

---

# Navigation Topics

## Robot Control

| Topic        | Type        | Description             |
| ------------ | ----------- | ----------------------- |
| `/cmd_vel`   | Twist       | Velocity commands       |
| `/goal_pose` | PoseStamped | Navigation goal         |
| `/plan`      | Path        | Planned navigation path |

## Sensor Data

| Topic   | Type      | Description     |
| ------- | --------- | --------------- |
| `/scan` | LaserScan | LiDAR scan data |
| `/odom` | Odometry  | Wheel odometry  |

## Mapping

| Topic  | Type          | Description        |
| ------ | ------------- | ------------------ |
| `/map` | OccupancyGrid | Generated SLAM map |

---

# Mapping Workflow

1. Launch the simulation environment
2. Run SLAM Toolbox to generate the map
3. Refine the map in GIMP for clean walls
4. Use the refined map for AMCL navigation

---

# Author

**Asif Morshed**

GitHub:
[https://github.com/morshed-asif](https://github.com/morshed-asif)

---
