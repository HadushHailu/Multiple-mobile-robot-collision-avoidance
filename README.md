# Motion Planning and Obstacle Avoidance for Multiple Mobile Robots

This project implements a **motion planning and obstacle avoidance algorithm** for multiple mobile robots. The system integrates **laser range data, clustering, Kalman filtering, and reciprocal velocity obstacles (RVO)** to enable robots to avoid dynamic obstacles and coordinate navigation in real time.  

Developed at the **University of Tsukuba (2021)** as part of research on autonomous multi-robot navigation.  

---

## Features
- Real-time motion planning and collision avoidance  
- Obstacle detection and clustering using **PCL (Point Cloud Library)**  
- Dynamic obstacle tracking with an **Extended Kalman Filter (EKF)**  
- Control integration with **Ypspur** for differential-drive robots  
- Real-time visualization with **gnuplot**  
- Logging of robot, obstacle, and via-point states for analysis  

---

## Project Structure
- **multi_robot_avoidance.cpp**  
  - **Main Thread**: Handles URG laser scanning, odometry input, and visualization with `gnuplot`  
  - **Avoidance Algorithm Thread**: Runs the obstacle detection, clustering, EKF prediction, and collision avoidance logic  
  - **Data Structures**:  
    - `urg_struct`: Laser scan points  
    - `obstacle_struct`: Obstacle center, time, and radius  
    - `viaPoints_struct`: Candidate avoidance via-points  
    - `cluster_struct`: Clustered obstacle information  

---

## Dependencies
Make sure the following libraries are installed:  

- **C++ Standard Library** (iostream, fstream, string, vector, math, thread, mutex, chrono, signal)  
- **PCL (Point Cloud Library)**  
- **Eigen3**  
- **Ypspur** (for mobile robot control)  
- **scip2awd** (for URG LIDAR)  
- **gnuplot** (for real-time plotting)  

Install on Ubuntu:  
```bash
sudo apt-get install libpcl-dev libeigen3-dev gnuplot

## Build
g++ -std=c++11 multi_robot_avoidance.cpp -o multi_robot_avoidance \
  -lpthread -lscip2awd -lypspur \
  $(pkg-config --cflags --libs pcl_common pcl_io eigen3)

## Run
./multi_robot_avoidance /dev/ttyACM0 
