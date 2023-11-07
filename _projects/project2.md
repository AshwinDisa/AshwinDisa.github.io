---
title: "Counter-UAV System"
excerpt: "Path planning and communication pipeline of a Drone interception system. <br/><img src='/images/counter_uav.png'>"
collection: projects
---

Implemented a follow and intercept algorithm in the velocity space as shown below. 

<br/><img src='/images/vel_space.png'>"

The velocity of the counter drone depends on 2 factors: 
:   velocity of rogue drone 
:   Distance to the rogue drone

A custom function is derived to estimate the velocity of the counter drone which depend on these two parameter. Once the counter UAV is in close vicinity of the rogue drone, the idea is to neutralize it by throwing a net module and return to base.

The system has been tested and validated using the following hardware after extensive testing in simulation environment (SITL). 
:   CubeOrange Flight controller with Ardupilot firmware
:   RaspBerrPi as the onboard computer running MAVROS to send direct velocity commands to FCU.

Following video shows the follow and interception visualization.

[<img src="https://i9.ytimg.com/vi/WRNtdgOR854/mqdefault.jpg?sqp=COCbqqoG-oaymwEmCMACELQB8quKqQMa8AEB-AH4BoAC0AWKAgwIABABGFsgZShcMA8=&rs=AOn4CLDPW8ycePypXzwacQ_8aUh3KS49GQ">](https://www.youtube.com/watch?v=WRNtdgOR854 "Counter UAV system")

Contributors: Suraj Bonagiri