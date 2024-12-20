# PRACTICE 4: DOCUMENTATION OF GLOBAL NAVIGATION

 Irene Diez de Toro
 
 November 2024 - Third Year of Robotic Software Robotics Engineering

# 0. INTRODUCTION

For this fourth assignment of the course, the goal of this practice is to develop a Gradient Path Planning (GPP) algorithm that enables a robot to navigate autonomously toward a selected destination. The robot must follow the shortest path while avoiding obstacles, such as non-road areas, ensuring safe and efficient movement. The system includes components like the city view, a graphical interface, the algorithm model, and a gallery for route simulations. The practice includes challenges to enhance the system’s functionality, such as ensuring the robot reliably reaches its destination, optimizing the algorithm to compute the shortest path efficiently, and minimizing the time taken to arrive. These objectives encourage refining the navigation logic for improved performance and adaptability.

a local navigation algorithm based on the ***"Virtual Force Field" (VFF)*** has been programmed for a Formula 1 car that moves around the track, avoiding any obstacles along the way. To detect obstacles and the boundaries of the track, the car is equipped with a **laser sensor** at the front. Additionally, there are several *waypoints* assigned on the track, which serve as *targets* that the car passes through until it reaches the finish line. These targets are used to generate an **attractive force vector** that guides the car towards each goal until it completes the lap. In this case, we were also asked, as a complementary but not primary task, to make the car as fast as possible, avoiding slow movement.


# 1. THEORICAL CONCEPTS

This exercise requires us to implement a global (and local) navigation using Motion Planning. Below is the complete theory that explains how to do it.

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

**--GLOBAL NAVIGATION--**

Motion Planning is a term used in robotics to find a sequence of valid configurations that moves the robot from source to destination. Motion Planning algorithms find themselves in a variety of settings, be it industrial manipulators, mobile robots, artificial intelligence, animations or study of biological molecules. There are mainly 2 methods to solve the exercise, Gradient Path Planning and Sampling Based Path Planning:

**GRADIENT PATH PLANNING**

One such method for Motion Planning is Gradient Path Planning. GPP works on the principle of potential fields. The obstacles in the path serve as potential wall to the path planner, and the target serve as potential well. By combining all the potential walls and wells, a path is constructed as a downward slope. The robot follows that path to reach it’s destination. Gradient Path Planning can be implemented using Brushfire Algorithm or Wave Front Algorithm. Next section explains the working of Wave Front Algorithm.

- ***Wave Front Algorithm***: is BFS based approach to build a path from source to destination. The algorithm works by assigning weights to a grid of cells. Given the source and target, the algorithm starts from the target node and moves outwards like a ripple, while progressively assigning weights to the neighboring cells.

- ***Assigning Weights***: As for obstacles, additional weights are added to the cells that are close to obstacles. Intuitively, the weights represent the superposition of waves that are reflected from the walls of obstacles.

- ***Superposition of Waves***: The algorithm stops upon reaching the source. To navigate through the generated path, the robot follows the path indicated by decreasing weights (a downhill drive). A grayscale image representation quite clearly depicts the path the robot might follow!

**SAMPLING BASED PATH PLANNING**

Sampling based Path Planning employs sampling of the state space of the robot in order to quickly and effectively plan paths, even with differential constraints or those with many degrees of freedom. Some of the algorithms under this class are:

- ***Probabilistic Roadmap***: These methods work by randomly sampling points in the workspace. Once the desired number of samples are obtained, the roadmap is constructed by connecting the random samples to form edges. On the resulting graph formed, any shortest path algorithm (A*, Dijkstra, BFS) is applied to get our resulting path.
 
- ***Tree Based Planner***: Tree Based Planners are very similar to Probabilistic Roadmaps, except for the fact that there are no cycles involved in tree based planners. There are a variety of tree based planners, like RRT, EST, SBL and KPIECE. These algorithms work heuristically, working from the root node, a tree (a graph without cycles) is constructed.


**--LOCAL NAVIGATION--**

Once the global path is decided, it is broken down into suitable waypoints. The robot navigates through these waypoints to reach its destination. Local Navigation involves a dynamically changing path plan, taking into consideration the changing surroundings and vehicle constraints. Some examples of such algorithms would be **Virtual Force Field**, **Follow Wall**, **Pledge Algorithm**, etc.

# 2. MY ALGORITHM
My algorithm is designed to implement an autonomous navigation system based on Gradient Path Planning (GPP) to efficiently guide a taxi toward a destination on a 2D map, avoiding obstacles and optimizing the route. The map, loaded as an image and converted into a 2D matrix, serves as the reference for calculating safe and efficient paths. The Breadth-First Search (BFS) algorithm is used to create a cost map, measuring the accumulated distance from the goal to each accessible cell in the map. Simultaneously, a penalty map is generated to increase costs around obstacles, expanding their influence area to ensure the taxi navigates safely, avoiding potential collisions.

The system operates in a continuous loop. First, it detects changes in the target, calculates the optimal route, and updates the cost and penalty maps. During navigation, it evaluates the taxi's neighboring cells, selects the move with the lowest cost, and adjusts the robot's linear and angular velocities to move in that direction. The map's absolute coordinates are converted into the taxi's relative frame for real-time movement planning. The Euclidean distance between the taxi and the target is constantly monitored to determine when to stop upon reaching the destination. Additionally, a graphical interface provides real-time visualization of the map, calculated costs, and the taxi's progress, allowing performance evaluation and navigation adjustments. This approach combines global planning and reactive navigation to achieve efficient and safe autonomous movement.

<p align="center">
  <img src="p4images/firstfinal3.png" alt="Final algorithm" width="70%" style="border: 2px solid black;">
  &nbsp;&nbsp;&nbsp;
</p>


# 3. THE PROCESS

During the creation of the program, I went through several important steps. First, to implement the map, it was necessary to develop the algorithm described in the theory of node expansion, Breadth-First Search (BFS). This step was not very difficult, as I had previously implemented this same algorithm in another course. Thanks to that prior experience, designing the main pseudocode was relatively straightforward. Next, I implemented a function to generate the child nodes from the current position, considering the possible movements both in a straight line and diagonally. During this process, I included the assignment of costs to each movement, distinguishing between diagonal and straight moves to accurately reflect the distance traveled. Finally, I integrated functionality to represent the progress made toward the target on the map, allowing real-time visualization of the algorithm's advancement. Below is an image illustrating this step of the process.

<p align="center">
  <img src="p4images/1.png" alt="Getting cost grid" width="70%" style="border: 2px solid black;">
  &nbsp;&nbsp;&nbsp;
</p>

In the following image, this same algorithm is shown with different targets.

<p align="center">
  <img src="p4images/firststeps2.png" alt="Target and resultant" width="70%" style="border: 2px solid black;">
  &nbsp;&nbsp;&nbsp;
</p>

The next step was to address the obstacles. This involved assigning a very high cost to the obstacle areas so that the taxi would avoid them during navigation. Additionally, it was necessary to expand the obstacles' influence area to increase the safety margin while the robot navigates. As I will mention in the challenges section, I went through several modifications before arriving at the current solution, which can be seen in the following images. The solution involves creating a separate map where the obstacles (and all their areas) are marked with high costs, while the paths are marked with zeros. This way, when the cost maps are combined, only the obstacle costs are added, and the paths remain clear, guiding the taxi around the obstacles efficiently.

<p align="center">
  <img src="p4images/firstversion.png" alt="First solution" width="40%" style="border: 2px solid black;">
  &nbsp;&nbsp;&nbsp;
  <img src="p4images/secondversion.png" alt="Second solution" width="40%" style="border: 2px solid black;">
  &nbsp;&nbsp;&nbsp;
</p>

Finally, the navigation step was implemented. This involved checking a movement window around the robot to evaluate the cost of the path in each cell, ensuring that the car moved toward the target without colliding with obstacles. The position of the robot on the map was constantly monitored to determine its next move. This part of the process wasn't very difficult to implement.To complete the navigation correctly, I had to increase the iterations of the expansion algorithm to prevent the robot from getting confused while navigating. The result of this final implementation can be seen in the following image.

<p align="center">
  <img src="p4images/apiece.png" alt="Final solution" width="50%" style="border: 2px solid black;">
  &nbsp;&nbsp;&nbsp;
</p>

# 4. DIFICULTIES

During the development of this project, I faced several challenges that affected the progress and implementation of the car’s navegation algorithm.

The first and main problem I encountered was understanding how to handle obstacles. Initially, I thought I should mark the expanded areas of the obstacles in black, without considering the need to assign costs to them only focusing on colors. As a result, the paths appeared narrower, but the obstacles didn’t have any costs, which caused issues during navigation. I soon realized this approach was incorrect because the obstacles were not properly accounted for in the cost grid, and the robot ended up colliding with walls. During development, I faced several setbacks that slowed down progress, such as other assignments and losing part of my code due to a Unibotics update. This caused delays, but eventually, I started working on a second version of the map. I initially thought assigning costs directly to the obstacles within the cost grid would solve the problem. However, this approach only applied the cost to the outer boundary of the obstacles, leaving the inside areas cost-free. As the robot navigated, it started colliding with the walls since it was still attempting to go through the obstacle areas. Also, there was no buffer zone or safety margin around the obstacles, so the robot got too close to them. After several attempts to modify the cost grid, I realized the solution was to invert the values into a separate map for the obstacles and combine it with the original cost grid. This approach allowed me to correctly mark the obstacles with high costs while keeping the paths clear for the robot to navigate safely.

Another issue I encountered was with the navigation. The taxi would only move towards nearby points, and when trying to reach distant targets, it would end up going in circles indefinitely. This wasn’t an obstacle-related problem, so after thinking about it and discussing it with some classmates, I realized that in class it had been mentioned that when expanding nodes, I should iterate a bit more after finding the target. This additional iteration ensured that the taxi wouldn’t get confused by the varying costs of the cells along the way. Implementing these extra iterations wasn’t too difficult, and it resolved the issue, allowing the taxi to navigate correctly towards the target without getting stuck.

<p align="center">
 <img src="p4images/finalmap.png" alt="Final map" width="60%" style="border: 2px solid black;">
  &nbsp;&nbsp;&nbsp;
</p>


# 5. VIDEO OF THE ALGORITHM

Click on the link to see it! -> [Global Navigation](https://urjc-my.sharepoint.com/:v:/g/personal/i_diezd_2022_alumnos_urjc_es/EQHPhi_y_B9IguEhNfkZYHYBv4xeNOz-l_AvXhLjtJ2DoA?nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0%3D&e=vZ7yfv) :)
