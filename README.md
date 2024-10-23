# Novus_Perception
Perception: Object Detection in a Simulation Environment
# Description
Implementation of an object detection and localization system using computer vision in a
Gazebo simulation. The goal is to detect and locate a specific object in the simulated environment using a camera mounted on a robot.

This readme file only includes the steps to run the ros packages and Gazebo visualization NOT the details about trials and experiments conducted.

[Report PDF file](Report_Novus_Assignment.pdf) is separately provided which includes all the detailed analysis.

# Docker ROS Noetic Workspace Setup

This repository contains instructions on how to set up a Docker environment with ROS Noetic and a Catkin workspace. The Dockerfile included in this repo installs necessary dependencies and creates a Catkin workspace for ROS development.

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/) installed on your machine
- [Visual Studio Code](https://code.visualstudio.com/) installed (optional but recommended)

## Getting Started

### Step 1: Clone or Create a Workspace
```bash
git clone https://github.com/rohitdhote111/Novus_Perception
cd 
```
### Step 2: Create a Docker image using dockerfile

- goto this repo folder 
- Create a docker image using Dockerfile

```bash 
docker  build -t r1_image .
```
This command will create image with "r1_image", we can check it inside list of images with command
```
docker images
```
### step 3: Create a Docker container using above image using bash file provided

First give write permission to bash file and then run it

```
chmod +x docker_run.bash
./docker_run.bash
```

### step 4: Copy required files

copy the packages present inside src folder from base machine to container src folder using cp command
Also copy lidar .bag file inside catkin_ws folder of the container
(Run below command outside container)

```
docker cp /path_to_folder/TII_Assignment/src/ r13d_container:/root/catkin_ws/
```

### step 5: Perform catkin_make

Goto catkin workspace and perform catkin_make 

```
cd ~/catkin_ws
catkin_make
```

### step 6: Run packages
  Two packages are present inside the src folder
 1. pointcloud_filer
 2. ransac_fast
we can run these packages using roslaunch command
```
roslaunch pointcloud_filer pointcloud_filter.launch
roslaunch ransac_fast ransac_fast.launch
```
### Rviz configuration
After Rviz windows is open select “Fixed Frame>mbuggy/base_link” from left side display panel

Add required pointclouds from Add>By topic>”select point required PC”

Increase point size. (0.03 is good)

Change color of the point cloud if required. (color transform>Flat then select color)


### To access docker container using new terminal window
Run below commands
```
docker exec -it r13d_container bash
cd ~/catkin_ws
source devel/setup.bash
