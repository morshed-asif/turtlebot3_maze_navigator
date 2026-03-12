📝 Project Overview

This repository contains a ROS 2 Humble workspace for simulating a TurtleBot3 Waffle navigating through a custom hexagonal "Sigma Maze." The project includes environment design, SLAM-based mapping refined via GIMP, and autonomous control using the Nav2 Python API.

🚀 Key Features

    Custom Environment: Hexagonal maze designed via Gazebo Building Editor.

    Waffle Configuration: Optimized for the TurtleBot3 Waffle model (Lidar + Camera).

    High-Fidelity Mapping: SLAM Toolbox maps refined in GIMP to ensure 100% wall occupancy.

    Autonomous Navigation: Programmatic goal setting via nav2_simple_commander.

🛠️ Installation & Workspace Setup

This project requires the turtlebot3_simulations package to be built from source within a local workspace to allow for custom world modifications.
1. Create Workspace & Clone Dependencies
Bash

mkdir -p ~/turtlebot3_ws/src
cd ~/turtlebot3_ws/src

# Clone the official simulation package
git clone -b humble https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git

# Clone this navigation project
git clone https://github.com/morshed-asif/turtlebot3_maze_navigator.git

2. Build and Source
Bash
cd ~/turtlebot3_ws
colcon build --symlink-install

# Add to your .bashrc for automatic sourcing
echo "source ~/turtlebot3_ws/install/setup.bash" >> ~/.bashrc
source ~/.bashrc

🕹️ How to Run
1. Launch Simulation

Ensure the model is set to Waffle:
Bash

export TURTLEBOT3_MODEL=waffle
ros2 launch turtlebot3_gazebo turtlebot3_my_maze.launch.py

2. Launch Navigation
Bash

ros2 launch turtlebot3_navigation2 navigation2.launch.py \
  use_sim_time:=True \
  map:=~/turtlebot3_maze_navigator/maps/sigma_maze.yaml

3. Run Mission Script
Bash

python3 ~/turtlebot3_maze_navigator/nav2_commander_api.py

📂 Repository Structure

    maps/: GIMP-refined .yaml and .pgm occupancy grids.

    src/: Custom launch files and Gazebo world descriptions.

    nav2_commander_api.py: Python navigation logic using BasicNavigator.
    
Author
Asif Morshed
