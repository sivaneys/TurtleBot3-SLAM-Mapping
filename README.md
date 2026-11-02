# TurtleBot3 Simulation in Gazebo

Spawns a TurtleBot3 (waffle_pi) into a custom Gazebo world containing a
box, a cylinder, and a wall obstacle — a self-contained simulation
project separate from the image-processing project.

## Prerequisites
- ROS 1 Noetic (Ubuntu 20.04, e.g. via WSL2)
- `turtlebot3`, `turtlebot3_msgs`, `turtlebot3_simulations` packages installed
- `gazebo_ros` package installed

## Setup

1. Copy this package into your catkin workspace:
   ```
   cp -r turtlebot3_sim_project ~/catkin_ws/src/
   ```

2. Build:
   ```
   cd ~/catkin_ws
   catkin_make
   source devel/setup.bash
   ```

## Run

```
export TURTLEBOT3_MODEL=waffle_pi
roslaunch turtlebot3_sim_project turtlebot3_custom_world.launch
```

This opens Gazebo with the TurtleBot3 spawned at the origin, facing a
red box, a blue cylinder, and a grey wall segment placed around it.

## Drive the robot around (teleoperation)

In a new terminal:
```
export TURTLEBOT3_MODEL=waffle_pi
roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```
Use the on-screen keys (w/a/s/d style controls) to drive the robot and
watch it navigate around the obstacles.

## Visualize sensors in RViz (optional)

```
roslaunch turtlebot3_bringup turtlebot3_model.launch
```
This shows the LIDAR scan and robot model without needing a physical robot.

## Useful checks
```
rostopic list              # /cmd_vel, /odom, /scan, /camera/rgb/image_raw
rostopic echo /odom         # live pose/velocity data as you drive
rqt_graph                   # visualize node/topic connections
```

## Notes
- Edit `worlds/turtlebot3_project.world` to add, move, or resize obstacles
  (box/cylinder/wall models) for different test scenarios.
- Change `x_pos`/`y_pos` launch args to spawn the robot at a different
  starting point in the world.
