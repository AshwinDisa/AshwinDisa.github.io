---
title: "Multi-Robot Coverage"
excerpt: "Coverage path planning of a multi-robot system in a rectangular grid with static known obstacles.<br/><img src='/images/mrcpp.png' width='400'/>"
collection: projects
---

Coverage path planning of a multi-robot system in a rectangular grid using voronoi partitioning technique to divide and assign areas. Known static obstacles are placed in the grid. Depth First Search (DFS) is implemented for coverage. 

### Obstacle avoidance using lidar for unknown obstacles

Added obstacles and a simple 'see obstacle deviate path' approch is implemented. Each robot is attached with a LIDAR which detects an obstacle, if its in path, the robot changes its course and comes back on the trajectory once it passes it. This is shown in the following video using 3 turtlebots in gazebo environment.

[<img src="/images/mrcpp2.png" width='400'/>](https://www.youtube.com/watch?v=trwM8ocZuMM "MR-CPP")

[Repository Link](https://github.com/AshwinDisa/CPP)  