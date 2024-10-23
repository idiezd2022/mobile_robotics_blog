
 # PRACTICE 3: DOCUMENTATION OF OBSTACLE AVOIDANCE

 Irene Diez de Toro
 
 October 2024 - Third Year of Robotic Software Robotics Engineering

# 0. INTRODUCTION

For this third assignment of the course, a local navigation algorithm based on the ***"Virtual Force Field" (VFF)*** has been programmed for a Formula 1 car that moves around the track, avoiding any obstacles along the way. To detect obstacles and the boundaries of the track, the car is equipped with a **laser sensor** at the front. Additionally, there are several *waypoints* assigned on the track, which serve as *targets* that the car passes through until it reaches the finish line. These targets are used to generate an **attractive force vector** that guides the car towards each goal until it completes the lap. In this case, we were also asked, as a complementary but not primary task, to make the car as fast as possible, avoiding slow movement.

**NOTE THAT:** In almost all the photos shown in this documentation, there is a problem with the colors. This is because, in class, the order of the vectors was unintentionally explained incorrectly when placing the function to represent the vectors. The only photo with the correct colors is the one shown in the description of my algorithm.


# 1. THEORICAL CONCEPTS

This exercise requires us to implement a local navigation algorithm called the **Virtual Force Field Algorithm**. Below is the complete theory regarding this algorithm.

**NAVIGATION**

**Robot Navigation** involves all the related tasks and algorithms required to take a robot from point A to point B autonomously without making any collisions. It is a well-studied topic in Mobile Robotics, comprising volumes of books! The problem of navigation is broken down into the following subproblems:

- **Localisation**: The robot needs to know where it is.
- **Collision Avoidance**: The robot needs to detect and avoid obstacles.
- **Mapping**: The robot needs to remember its surroundings.
- **Planning**: The robot needs to be able to plan a route to point B.
- **Explore**: The robot needs to be able to explore new terrain.

**ROBOT NAVIGATION PROBLEMS**

Some of the ways to achieve the task of navigation are as follows:

- **Vision-Based**: Computer Vision algorithms and optical sensors, like LIDAR sensors, are used for Vision-Based Navigation.
- **Inertial Navigation**: Airborne robots use inertial sensors for Navigation.
- **Acoustic Navigation**: Underwater robots use SONAR-based Navigation Systems.
- **Radio Navigation**: Navigation using RADAR technology.

The problem of **Path Planning** in navigation is dealt with in two ways: **Global Navigation** and **Local Navigation**.

**GLOBAL NAVIGATION**

Global Navigation involves the use of a map of the environment to plan a path from point A to point B. The optimality of the path is based on the length of the path, the time taken to reach the target, using permanent roads, etc. Global Positioning System (GPS) is one example of Global Navigation. The algorithms used in such systems may include Dijkstra, Best First, or A*, etc.

**LOCAL NAVIGATION**

Once the global path is decided, it is broken down into suitable waypoints. The robot navigates through these waypoints to reach its destination. Local Navigation involves a dynamically changing path plan, taking into consideration the changing surroundings and vehicle constraints. Some examples of such algorithms would be **Virtual Force Field**, **Follow Wall**, **Pledge Algorithm**, etc.

**VIRTUAL FORCE FIELD ALGORITHM**

The **Virtual Force Field Algorithm** works in the following steps:

1. The robot assigns an **attractive vector** to the waypoint that points towards the waypoint.
2. The robot assigns a **repulsive vector** to the obstacle according to its sensor readings that points away from the waypoint. This is done by summing all the vectors that are translated from the sensor readings.
3. The robot follows the vector obtained by summing the target and obstacle vectors.

**DETERMINING THE VECTORS**

- **Target Vector**: The target vector can be easily obtained by subtracting the position of the car from the position of the next waypoint. In order to implement this on the GUI interface of the exercise, in addition to the vector obtained by subtracting, we need to apply a rotation to the vector as well. The purpose of rotation is to keep the target vector always in the direction of the waypoint and not in front of the car.
- **Obstacle Vector**: The obstacle vector is to be calculated from the sensor readings we obtain from the surroundings of the robot. Each obstacle in front of the car, is going to provide a repulsive vector, which we will add to obtain the resultant repulsive vector. Assign a repulsive vector, for each of the 180 sensor readings. The magnitude of the repulsive vector is inversely proportional to the magnitude of the sensor reading. Once, all the repulsive vectors are obtained they are all added, to get the resultant.
- **Direction Vector**: To obtain the direction vector we should add the target vector and the obstacle vector. But, due to an inherent problem behind the calculation of the obstacle vector, we cannot simply add them to obtain the resultant. We are required to keep moving forward for the purpose of this exercise. Hence, the component of the direction vector in the direction of motion of the car, has no effect on the motion of the car. Therefore, we can simply leave it as a constant, while adjusting the vector responsible for the steering of the car. It is the steering, that will in fact, provide us with the obstacle avoidance capabilities. Hence, the steering is going to be controlled by the Direction Vector.

# 2. MY ALGORITHM
My algorithm is designed to control the movement of a robot using an approach based on *attractive* and *repulsive forces*. I initialize two parameters, **ALPHA** and **BETA**, which weigh the influence of each force on the robot's movement. Then, I calculate a repulsive vector based on the laser sensor readings, where the repulsion is stronger as obstacles get closer. I also convert the target coordinates into the robot's local reference frame and limit the magnitude of the vectors to avoid abrupt movements. In a main loop, I obtain the robot's current position and the target coordinates, calculate the distance between them, and compute the attractive and repulsive forces. If the robot is close to the target, I mark it as reached; otherwise, I calculate a *resultant force vector* and use it to direct the robot's movement. Additionally, I display the forces on the graphical interface to monitor the robot's behavior. The image shows the final vectors during the program.

<p align="center">
  <img src="p3images/finalvectors.png" alt="Final vectors" width="70%" style="border: 2px solid black;">
  &nbsp;&nbsp;&nbsp;
</p>


# 3. THE PROCESS

During the creation of the program, I went through several important steps. First, I developed the *attraction vector*. In this case, I didn't take long to implement it, as it only involved transferring the coordinates of the car and the target. However, without realizing it, this implementation wasn't entirely correct and would cause problems later on, as can be seen in the first image.

<p align="center">
  <img src="p3images/gettarget.png" alt="Getting target vector" width="70%" style="border: 2px solid black;">
  &nbsp;&nbsp;&nbsp;
</p>

The second step was to create the *repulsion vector* using the values from the laser. At this point, I made numerous modifications due to calculation errors, which are detailed later in the difficulties section. Finally, I calculated the *resulting vector*. This last step did not present me with significant difficulties, as I only needed to adjust the coefficient values in the sum a couple of times until I found the correct ones.

However, as shown in the image and described in the process of creating the repulsion vector, in the first functional version I developed, I could only detect obstacles that were very close. This meant that when there were no visible obstacles, the resulting vector appeared incorrectly. Once I made the necessary changes, I was able to adjust the car's speed (initially, I considered deriving it from the resulting vector, but that wasn't viable) and the direction, which is based on the angle of that vector.

<p align="center">
  <img src="p3images/getingtargetresultant.png" alt="Target and resultant" width="70%" style="border: 2px solid black;">
  &nbsp;&nbsp;&nbsp;
</p>

In the last image, you can see that I was practically close to solving the problem. As observed, the repulsion vector was well-scaled, but the attraction vector was too long, giving it too much influence on the resulting vector. This caused the movement to be uncontrolled and the robot not to avoid obstacles properly. Ultimately, I understood that I also needed to limit the attraction vector to balance both vectors and make the algorithm work correctly.

<p align="center">
  <img src="p3images/nearsolution.png" alt="Near solution" width="70%" style="border: 2px solid black;">
  &nbsp;&nbsp;&nbsp;
</p>


# 4. DIFICULTIES

During the development of this project, I faced several challenges that affected the progress and implementation of the car’s navegation algorithm.

The biggest problem I faced was obtaining and generating the **repulsive vector**, which is derived from the laser sensor data. At first, I struggled a lot to understand the concept related to the laser theory, as I didn’t have the opportunity to work with it in the first exercise, and last year, when we covered it in another subject, I didn’t fully grasp it.

After several days of analyzing it and with the help of the code I already had, I managed to create an initial vector. In that case, I took the laser values, calculated the corresponding components, and summed them. I noticed that it was necessary to invert the values since the force needed to push in the opposite direction. This process took me quite a bit of time before I got it to work correctly.

When the vector began to work relatively well, obstacles were successfully avoided, except in the case of distant targets, where the robot would get stuck to a wall and wouldn’t move away. After hearing a classmate’s question and the professor's response, I realized that my calculation was incorrect. What I actually needed to do was calculate the *inverse* and the *average* of the distances, so that all the distances were taken into account, but with the closest ones having the most influence.

After a few adjustments, I managed to solve the issue and optimize the calculation. Below are two images of the vectors I had initially generated:

<p align="center">
 <img src="p3images/badvectors2.png" alt="Second fail vector" width="30%" style="border: 2px solid black;">
  &nbsp;&nbsp;&nbsp;
  <img src="p3images/ badvectors.png" alt="First fail vector" width="45%" style="border: 2px solid black;">
  &nbsp;&nbsp;&nbsp;
</p>


# 5. VIDEO OF THE ALGORITHM

Click on the link to see it! -> [Obstacle Avoidance](https://urjc-my.sharepoint.com/:v:/g/personal/i_diezd_2022_alumnos_urjc_es/EeKXJ6TyTSNCtE7tKXGNhtgBUMw1IQSRlZi493xc5sVbdA?e=vJyW6k&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0%3D) :)
