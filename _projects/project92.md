---
title: "OpenManipulatorX with ROS2"
excerpt: "Forward, Inverse, Velocity Kinematics of a 4 dof manipulator.<br/><img src='/images/openmanipulatorX.jpg' width='400'/>"
collection: projects
---

### Forward Kinematics
Given the joint angles, the goal is to estimate the end -effector position.

The DH parameters table used for Forward Kinematics is shown here.

<br/><img src='/images/dh.png'>"

The equations to obtain the x, y and z coordinates of the end-effector are - 

```
# q1, q2, q3, q4 are the joint angles in radians.

x = math.cos(q1) * (133.4*math.cos(q2+q3+q4) + 130.2*(math.cos(q2 - 1.39)) + 124*math.cos(q2+q3))
y = math.sin(q1) * (133.4*math.cos(q2+q3+q4) + 130.2*(math.cos(q2 - 1.39)) + 124*math.cos(q2+q3))
z = 48163/500 - (651*math.sin(q2 - 139/100))/5 - 124*math.sin(q2 + q3) - (667*math.sin(q2 + q3 + q4))/5
```

### Inverse Kinemtics
Given the end-effector positions in x, y, z, the goal is to estimate the joint angles.
This was done using analytical/geometric approach. The 4 dof problem of broken down into a 3-link planar chain (for q2, q3, q4) and a yaw (for q1) problem. The algorithm makes sure that the end-effector joint always faces down rather an arbitrary orientation, which makes pick/place easier. The following code snippet shows the code to calculate the joint angles.

```
def inverse_kinematics(self, xe, ye, ze, gamma):

    l12 = 130.23
    l23 = 124
    l34 = 133.4
    offset = 79.38

    g = np.radians(gamma)

    J1a, J2a, J3a = 0.0, 0.0, 0.0

    theta1 = math.atan(ye/xe)

    x3 = xe - (l34*math.cos(g))
    z3 = ze - (l34*math.sin(g))
    c = math.sqrt(x3**2 + z3**2)

    if ((l12 + l23) > c):

        a = math.acos((l12**2 + l23**2 - c**2)/(2*l12*l23))
        B = math.acos((l12**2 + c**2 - l23**2)/(2*l12*c))

        # elbow-down
        J1a = -(math.atan(z3/x3)-B - np.radians(offset))
        J2a = -(math.pi-a + np.radians(offset))
        J3a = -(g - J1a -J2a)

        # elbow-up
        J1b = -(math.atan(z3/x3)+B - np.radians(offset))
        J2b = math.pi-a -np.radians(offset)

        J1b_new = math.atan(z3/x3) + B
        J2b_new = -(math.pi - a)

        J3b_new = -(g - J1b_new - J2b_new)

    else:
        print("dimension error!")

    angles = np.array([theta1, J1b, J2b, J3b_new])

    return angles


```

### Velocity Kinematics
Given the end-effector velocity in 3d, the goal is to find the individual joint velocities using a Jacobian matrix. The following code snippet shows the construction of the Jacobian matrix.

```
def makeJacobian(self, q1, q2, q3, q4):

    L12 = 96.326
    L3 = 130.23
    L4 = 124
    L5 = 133.4

    # assume joint positions are passed in as radians
    
    q2preload = math.radians(10.807)
    q34preload = math.radians(90)
    
    x_star = (L3 * math.sin(q2 + q2preload)) + (L4 * math.sin(q2+q3+q34preload)) + (L5 * math.sin(q2+q3+q4+q34preload))
    
    q4xy = L5 * math.cos(q2+q3+q4+q34preload)
    q3xy = q4xy + (L4 * math.cos(q2+q3+q34preload))
    q2xy = q3xy + (L3 * math.cos(q2+q2preload))
    
    q4z = -(L5 * math.sin(q2+q3+q4+q34preload))
    q3z = q4z - (L4*math.sin(q2+q3+q34preload))
    q2z = q3z - (L3*math.sin(q2+q2preload))
    
    c1 = math.cos(q1)
    s1 = math.sin(q1)
    
    #                       q1dot       q2dot       q3dot       q4dot
    jacob = np.array([[-x_star * s1,  c1 * q2xy,  c1 * q3xy,  c1 * q4xy],   # x
                        [ x_star * c1,  s1 * q2xy,  s1 * q3xy,  s1 * q4xy],   # y
                        [           0,        q2z,        q3z,        q4z]])  # z

    return jacob
```

[Github repo link](https://github.com/AshwinDisa/OpenManipulatorX_ROS2)

[<img src="/images/openmanipulatorX.jpg">](https://youtube.com/shorts/_iANV6D9pfc "Pick and Place using Inverse Kinematics")

Contributors: Samuel Rooney, Pingze He

Final project for RBE500 - Foundations of Robotics Fall 2023 by Prof. Berk Calli at WPI.
