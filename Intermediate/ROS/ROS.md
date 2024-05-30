
# Ardupilot 
ArduPilot enables the creation and use of trusted, autonomous, unmanned vehicle systems for the peaceful benefit of all. ArduPilot provides a comprehensive suite of tools suitable for almost any vehicle and application. As an open source project, it is constantly evolving based on rapid feedback from a large community of users. The Development Team works with the community and commercial partners to add functionality to ArduPilot that benefits everyone. Although ArduPilot does not manufacture any hardware, ArduPilot firmware works on a wide variety of different hardware to control unmanned vehicles of all types. Coupled with ground control software, unmanned vehicles running ArduPilot can have advanced functionality including real-time communication with operators. ArduPilot has a huge online community dedicated to helping users with questions, problems, and solutions.

_**Community is what really sets ArduPilot apart from many other offerings in the market.**_

### Features
- Thorough documentation of the available features backed by a community to help you set up any vehicle to fit your needs.
- Many command modes to fit every type of vehicle: Acro, Stabilize, Loiter, Alt-hold, Return To Launch, Land, Follow Me, GeoFence, etc.
- Autonomous flight modes that execute fully scripted missions with advanced features.
- Advanced failsafe options bring peace of mind in the event of lost control signal, low battery conditions, or other system failures.
  For more info you can checkout [ardupilot](https://ardupilot.org/ardupilot/)

### Before continuation you should install [ardupilot](https://github.com/Bhaveshmeghwal21/AMC_Summer_Camp-2024/blob/main/Intermediate/ROS/Ardupilot-installation.md)



# SITL
The SITL (software in the loop) simulator allows you to run Plane, Copter or Rover without any hardware. It is a build of the autopilot code using an ordinary C++ compiler, giving you a native executable that allows you to test the behaviour of the code without hardware.
SITL allows you to run ArduPilot on your PC directly, without any special hardware. It takes advantage of the fact that ArduPilot is a portable autopilot that can run on a very wide variety of platforms. Your PC is just another platform that ArduPilot can be built and run on.
When running in SITL the sensor data comes from a flight dynamics model in a flight simulator. ArduPilot has a wide range of vehicle simulators built in, and can interface to several external simulators. This allows ArduPilot to be tested on a very wide variety of vehicle types. For example, SITL can simulate:
- multi-rotor aircraft
- fixed wing aircraft
- ground vehicles
- underwater vehicles
- camera gimbals
- antenna trackers
- a wide variety of optional sensors, such as Lidars and optical flow sensors


![](https://ardupilot.org/dev/_images/ArdupilotSoftwareintheLoopSITL.jpg)
