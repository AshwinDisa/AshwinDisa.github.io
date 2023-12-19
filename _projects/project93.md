---
title: "Centralized Multi-Robot Path Planning using dRRT Algorithm"
excerpt: "Plan a path for multiple robots simultaneously by treating the robots as a single composite system with many degrees of freedom.<br/><img src='/images/mujoco.png' width='500'/>"
collection: projects
---

Abstract—This project aims to plan a path for multiple robots simultaneously by treating the robots as a single composite system with many degrees of freedom, known as centralized multi-robot planning. The plan is to utilize dRRT (discrete Rapidly Exploring Random Tree) algorithm over preplanned single robot PRM (Probabilistic Roadmap) graphs. Instead of doing a tree search over the entire cartesian workspace and performing expensive collision checks over and over again, we are planning over a environment-collision free state subset obtained via the tensor product of individual robot PRMs. 

[Download report here](/files/Motion_Planning_Final_Report.pdf),  [Github repo link](https://github.com/AshwinDisa/Multi_robot_centralized_planning)

Contributors: Manoj Velmurugan

Final project for RBE550 - Motion Planning by Prof. Constantinos Chamzas at WPI.
