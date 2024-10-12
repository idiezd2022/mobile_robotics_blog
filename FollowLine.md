# PRACTICE 2: DOCUMENTATION OF FOLLOW LINE

 Irene Diez de Toro
 
 October 2024 - Third Year of Robotic Software Robotics Engineering


# 0. INTRODUCTION

For this second project, the objective was to program a control algorithm for a **formula 1** car. To achieve this, the car had to detect, using a forward-facing color camera, a red line in the center of the lane and follow it. We had to implement code that processed the images returned by the camera to be able to follow the red line painted on the lane. Additionally, we had to program a control command generator for the linear and angular velocities through a PID in order to steer the car to the finish line in the shortest time possible. Moreover, as a special case, we could implement an extra behavior so that when the car lost the line, it could find it again.

# 1. THEORICAL CONCEPTS

DETECTING LINE

The first task of the assignment is to detect the line to be followed. This can be achieved easily by filtering the color of the line from the image and applying basic image processing to find the point or line to follow, or in Control terms our Set Point. Using color filter like HSV.

CONTROL SYSTEM

A system of devices or set of devices, that manages, commands, directs or regulates the behavior of other devices or systems to achieve the desired results. Simply speaking, a system which controls other systems. Control Systems help a robot to execute a set of commands precisely, in the presence of unforeseen errors. Types of Control System:

 - Open Loop Control System: A control system in which the control action is completely independent of the output of the system. A manual control system is on Open Loop System.
 - Closed Loop Control System: A control system in which the output has an effect on the input quantity in such a manner that the input will adjust itself based on the output generated. An open loop system can be converted to a closed one by providing feedback.
 - PID Control: A control loop mechanism employing feedback. A PID Controller continuously calculates an error value as the difference between desired output and the current output and applies a correction based on proportional, integral and derivative terms(denoted by P, I, D respectively).
     - Proportional: Proportional Controller gives an output which is proportional to the current error. The error is multiplied with a proportionality constant to get the output. And hence, is 0 if the error is 0.
     - Integral: Integral Controller provides a necessary action to eliminate the offset error which is accumulated by the P Controller.It integrates the error over a period of time until the error value reaches to zero.
     - Derivative: Derivative Controller gives an output depending upon the rate of change or error with respect to time. It gives the kick start for the output thereby increasing system response.


# 2. MY ALGORITHM


# 3. THE PROCESS


# 4. DIFICULTIES

During the development of this project, I faced several challenges that affected the progress and implementation of the car's control algorithm.

First, I had difficulties with image filtering. At the beginning, I didn’t fully understand how to extract the desired color from the image and then follow it. Even though I had the reference code provided by the professor and available documentation, it took me some time to correctly adjust the color filter and get the appropriate values in the RGB color space. Additionally, in one of the classes, the professor suggested that I focus on a specific region of the red line to facilitate tracking. Initially, I couldn’t implement this correctly, which caused the car to struggle with following the line accurately. Eventually, I managed to solve this by focusing on a single point within the red line region to calculate the positional error, which significantly improved the tracking performance.

Another major challenge was the implementation of the PID controller. When I started working on this, I didn’t have a clear understanding of how it worked, as the theory behind PID hadn’t yet been covered in class. To overcome this, I decided to research on my own. I consulted technical documentation and websites that explained the PID theory, which allowed me to grasp the basic concepts and how to implement it in my code. However, adjusting the constant values (the proportional, integral, and derivative "K" values) was particularly tricky, especially in curves, where controlling the car’s behavior was more challenging.

Lastly, the other circuits I worked with were more complex. The Ackerman maps, in particular, were very difficult for me to understand, especially in terms of how to adjust the values and efficiently control the car in those environments. Due to the complexity of adapting my code for those circuits, I decided not to focus on them and instead optimize my solution for the simpler circuits.

# 5. VIDEO OF THE ALGORITHM

Click on the link to see it! -> [Follow line f1](https://urjc-my.sharepoint.com/:v:/g/personal/i_diezd_2022_alumnos_urjc_es/EW1LQheTLhBDkasUOvaXDXQBFv_15ddIiCYSZQSe-a8Seg?nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0%3D&e=MjNSFI) :)
