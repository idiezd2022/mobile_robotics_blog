# PRACTICE 2: DOCUMENTATION OF FOLLOW LINE

 Irene Diez de Toro
 
 October 2024 - Third Year of Robotic Software Robotics Engineering


# 0. INTRODUCTION

For this second project, the objective was to program a control algorithm for a **formula 1** car. To achieve this, the car had to detect, using a forward-facing color camera, a red line in the center of the lane and follow it. We had to implement code that processed the images returned by the camera to be able to follow the red line painted on the lane. Additionally, we had to program a control command generator for the linear and angular velocities through a PID in order to steer the car to the finish line in the shortest time possible. Moreover, as a special case, we could implement an extra behavior so that when the car lost the line, it could find it again.

# 1. THEORICAL CONCEPTS

DETECTING LINE

The first task of the assignment is to detect the line to be followed. This can be achieved easily by filtering the color of the line from the image and applying basic image processing to find the point or line to follow, or in Control terms our Set Point. Using color filter like HSV.

CONTROL SYSTEM

A system of devices or set of devices, that manages, commands, directs or regulates the behavior of other devices or systems to achieve the desired results. Simply speaking, a system which controls other systems. Control Systems help a robot to execute a set of commands precisely, in the presence of unforeseen errors.

Types of Control System

 - Open Loop Control System: A control system in which the control action is completely independent of the output of the system. A manual control system is on Open Loop System.
 - Closed Loop Control System: A control system in which the output has an effect on the input quantity in such a manner that the input will adjust itself based on the output generated. An open loop system can be converted to a closed one by providing feedback.
 - PID Control: A control loop mechanism employing feedback. A PID Controller continuously calculates an error value as the difference between desired output and the current output and applies a correction based on proportional, integral and derivative terms(denoted by P, I, D respectively).
     - Proportional: Proportional Controller gives an output which is proportional to the current error. The error is multiplied with a proportionality constant to get the output. And hence, is 0 if the error is 0.
     - Integral: Integral Controller provides a necessary action to eliminate the offset error which is accumulated by the P Controller.It integrates the error over a period of time until the error value reaches to zero.
     - Derivative: Derivative Controller gives an output depending upon the rate of change or error with respect to time. It gives the kick start for the output thereby increasing system response.


# 2. MY ALGORITHM


# 3. THE PROCESS


# 4. DIFICULTIES


# 5. VIDEO OF THE ALGORITHM

Click on the link to see it! -> [Follow line f1]() :)
