# Simulation 
Simulation is the process of mathematical modelling, performed on a computer, which is designed to predict the behaviour of, or the outcome of, a real-world or physical system. The reliability of some mathematical models can be determined by comparing their results to the real-world outcomes they aim to predict.

## Why simulation in aerial robotics?
Simulation is an important step in the development of drones. Here are some key reasons why simulations are important: 
- **Safety**: Simulations allow for the testing of drone systems and maneuvers in a virtual environment, reducing the risk of crashes and damage to the actual hardware. This is especially important for beginners and in complex scenarios where real-world testing might be dangerous.
- **Cost-Effective**: Developing and testing drones in a simulated environment can save significant costs associated with prototype development, repairs, and maintenance. It also reduces the need for extensive physical testing.
- **Training**: Simulations provide a risk-free platform for training new pilots. You can practice flying, navigating obstacles, and handling emergency situations without the fear of damaging the drone or injuring themselves.
- **Scenario Testing**: Simulations enable the testing of various scenarios and conditions that might be difficult or impossible to recreate in the real world. This includes extreme weather conditions, complex terrains, and emergency situations.
- **Design and Development**: Engineers and developers use simulations to test new designs, algorithms, and technologies. They can simulate the performance of different components and systems to optimize the drone’s efficiency and functionality.
- **Autonomous Systems**: For drones that operate autonomously, simulations are essential for testing navigation algorithms, sensor integration, and decision-making processes. It ensures that the drone can perform tasks reliably without human intervention.
- **Data Collection and Analysis**: Simulations generate valuable data that can be analyzed to improve drone performance and safety. This data helps in understanding how drones respond to different conditions and scenarios, leading to better design and operation strategies.

# Robot Operating System (ROS)
The Robot Operating System (ROS) is a set of software libraries and tools that help you build robot applications. From drivers to state-of-the-art algorithms, and with powerful developer tools, ROS has what you need for your next robotics project. And it's all open source.
(_Reference https://www.ros.org/_)

![](https://github.com/Bhaveshmeghwal21/GIFs/blob/main/gif_summer_camp/ROS_logo.png) 

Before moving ahead go through the [Basic linux Commands](https://www.geeksforgeeks.org/basic-linux-commands/) and complete the installation process from [here](https://github.com/Bhaveshmeghwal21/AMC_Summer_Camp-2024/blob/main/Windows.pdf)

![](https://github.com/Bhaveshmeghwal21/GIFs/blob/main/gif_summer_camp/exciting3.gif)

After completing the installation process, use the following command in ubuntu 20.04 LTS terminal to check
```bash
roscore 
```
the output should be similar to this 

![](https://github.com/Bhaveshmeghwal21/GIFs/blob/main/gif_summer_camp/roscore-04-1024x501.png)


Go through the [ROS basic commands](https://wiki.ros.org/ROS/Tutorials/NavigatingTheFilesystem)
# ROS tutorials
**NOTE** You should also follow these video tutorials for complete ROS [beginner](https://www.youtube.com/playlist?list=PL868twsx7OjdnroeAUFVBGlKGnFGi9txc) (watch only from 2-9)
- [creating a ROS package](https://wiki.ros.org/ROS/Tutorials/CreatingPackage)
- [Building a ROS package](https://wiki.ros.org/ROS/Tutorials/BuildingPackages)
- [ROS Nodes](https://wiki.ros.org/ROS/Tutorials/UnderstandingNodes)
- [ROS Topics](https://wiki.ros.org/ROS/Tutorials/UnderstandingTopics)

## Practice 1
Terminal 1
```bash
roscore
```
Terminal 2
```bash
rosrun turtlesim turtlesim_node
```
Turtle should be spawned

Terminal 3  
```bash
rostopic pub -r 1 /turtle1/cmd_vel geometry_msgs/Twist "linear:
  x: 1.0
  y: 0.0
  z: 0.0
angular:
  x: 0.0
  y: 0.0
  z: 1.0" 
```
Your turtle should move
Note that 
- -r 1 means it will publish at the rate of 1 Hz _(check out [rostopic](http://wiki.ros.org/rostopic)]_
- /turtle/cmd_vel is a topic and geometry_msgs/Twist is a msg type (data type). Don't worry you will understand later in this tutorial

Terminal 4
```bash
rosrun turtlesim turtle_teleop_key
```
Now you can also control your turtle with arrows key

To reset, type 
```bash
rosservice call /reset
```
At last type 
```bash
rosrun rqt_graph rqt_graph
```
You should see something like this
![rqt](https://github.com/Bhaveshmeghwal21/GIFs/blob/main/gif_summer_camp/turtlesim.png)

Now you can go on
- [ROS Services and Parameters](https://wiki.ros.org/ROS/Tutorials/UnderstandingTopics)
- [rqt console and roslaunch](https://wiki.ros.org/ROS/Tutorials/UsingRqtconsoleRoslaunch)
- [msg](https://wiki.ros.org/msg)
- [srv](https://wiki.ros.org/srv)
- [creating a ROS msg and srv](https://wiki.ros.org/ROS/Tutorials/CreatingMsgAndSrv)
- [Examining the simple publisher and subscriber](https://wiki.ros.org/ROS/Tutorials/ExaminingPublisherSubscriber)
- [Writing a simple publisher and subscriber (Python)](http://wiki.ros.org/ROS/Tutorials/WritingPublisherSubscriber%28python%29)
- [Examining the simple service and client](https://wiki.ros.org/ROS/Tutorials/WritingServiceClient%28python%29)
- [Writing the simple service and client (python)](https://wiki.ros.org/ROS/Tutorials/WritingServiceClient%28python%29)


# Task 1
Create a python script to run the turtle in square shape like this
![](https://github.com/Bhaveshmeghwal21/GIFs/blob/main/gif_summer_camp/Screenshot%20from%202024-05-27%2018-19-05.png)



