# Visual SLAM with Tello

## Overview
This project aims to implement Visual SLAM (Simultaneous Localization and Mapping) using a Tello drone equipped with a monocular camera.

## Project Description
The project integrates the following components:
- **Hardware:** DJI Tello Drone
- **Software:** ROS Melodic, Visual SLAM algorithms (e.g., ORB-SLAM, LSD-SLAM)
- **Tasks:**
  - Establish communication between ROS and Tello for sensor data retrieval and control.
  - Implement Visual SLAM algorithms for mapping and localization.
  - Real-time visualization of the generated map in ROS Rviz.
  - Autonomous navigation using mapped data and obstacle avoidance.

## Technical Details
### Dependencies
- ROS Melodic
- Tello ROS package for interfacing with the Tello drone
- Visual SLAM libraries (e.g., ORB-SLAM2, LSD-SLAM)

### Setup Instructions
1. Install ROS Melodic on your system.
2. Clone the Tello ROS package repository and install dependencies.
3. Install and configure the selected Visual SLAM library.
4. Configure the network for communication with the Tello drone.
5. Launch ROS nodes for drone control, camera data, and Visual SLAM.

### Project Goals
- Achieve accurate localization and mapping in diverse indoor environments.
- Develop a robust system for autonomous navigation and obstacle avoidance.
- Optimize Visual SLAM algorithms for real-time performance on resource-limited platforms.
- Create a reusable and extendable software architecture for future drone projects.
