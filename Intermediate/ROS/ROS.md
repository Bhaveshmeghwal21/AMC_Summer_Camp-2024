
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
Adding new simulated vehicle types or sensor types is straightforward.

A big advantage of ArduPilot on SITL is it gives you access to the full range of development tools available to desktop C++ development, such as interactive debuggers, static analyzers and dynamic analysis tools. This makes developing and testing new features in ArduPilot much simpler.

![](https://ardupilot.org/dev/_images/ArdupilotSoftwareintheLoopSITL.jpg)

# Copter SITL/MAVProxy Tutorial
## MAVProxy
For those wondering why there is a map when you launch SITL, well it is due to MAVProxy.
MAVProxy is a fully-functioning GCS for UAV’s, designed as a minimalist, portable and extendable GCS for any autonomous system supporting the MAVLink protocol (such as one using ArduPilot). MAVProxy is a powerful command-line based “developer” ground station software. It can be extended via add-on modules, or complemented with another ground station, such as Mission Planer, APM Planner 2, QGroundControl etc, to provide a graphical user interface.

Now launch SITL
```bash
cd ~/ardupilot/ArduCopter
sim_vehicle.py --map --console
```
Note that by default Copter is being started, well it is because your directory is ```~/ardupilot/ArduCopter``` 
The MAVProxy Command Prompt, Console and Map should be arranged conveniently so you can observe the status and send commands at the same time.

![](https://ardupilot.org/dev/_images/mavproxy_sitl_console_and_map.jpg)


**Tips**
- You can also change your frame in using ```-f``` paramter. A complete list of startup options for the simulator can be found using the –help option:
```bash
sim_vehicle.py --help
```
- Also if you want to change your quad start location, you can start the simulator with the vehicle at a particular location by calling sim_vehicle.py with the ```-L``` parameter and a named location in the ```~/ardupilot/Tools/autotest/locations.txt``` file.

You can add your own locations to the file. The order is Lat,Lng,Alt,Heading where alt is MSL and in meters, and heading is degrees.
for eg add ```Vivekananda=25.259073,82.986746,84.2,0``` in ```~/ardupilot/Tools/autotest/locations.txt```

then
```bash
cd ~/ardupilot/ArduCopter && sim_vehicle.py -L Vivekananda --console --map
```

TADAMM!!! now you can see that start location of your drone is at the centre of the Vivekananda Hostel 

_for more check out [Using sim_vehicle.py](https://ardupilot.org/dev/docs/using-sitl-for-ardupilot-testing.html#using-sim-vehicle-py)_

## Taking off
This section explains how to take off in ```GUIDED``` mode. The main steps are to change to ```GUIDED``` mode, arm the throttle, and then call the ```takeoff``` command. **Takeoff must start within 15 seconds of arming, or the motors will disarm!**

**NOTE** At time of writing, Copter only supports takeoff in guided mode; if you want to fly a mission you first have to take off and then switch to AUTO mode. For more flight modes you can check out [Flight Modes](https://ardupilot.org/copter/docs/flight-modes.html)

Enter the following commands in the MAVProxy Command Prompt.
```bash
mode guided
arm throttle
takeoff 40
```
Copter should take off to an altitude of 40 metres and then hover (while it waits for the next command).

## Changing flight mode - circle and land
The command below shows how to put Copter into [CIRCLE](https://ardupilot.org/copter/docs/circle-mode.html#circle-mode) mode with a [CIRCLE_RADIUS](https://ardupilot.org/copter/docs/parameters.html#circle-radius) of 2000cm. This will fly the Copter in a circle at a constant altitude, with the front pointed towards the centre of the circle.

```bash
mode circle
param set circle_radius 2000
```

**NOTE** If you set the CIRCLE_RADIUS to zero the vehicle will rotate in place.

Copter supports a [number of other flight modes]((https://ardupilot.org/copter/docs/flight-modes.html#flight-modes), which you can list in MAVProxy using the ```mode``` command:
```bash
mode
Available modes:  dict_keys(['STABILIZE', 'ACRO', 'ALT_HOLD', 'AUTO', 'GUIDED', 'LOITER', 'RTL', 'CIRCLE', 'POSITION', 'LAND', 'OF_LOITER', 'DRIFT', 'SPORT', 'FLIP', 'AUTOTUNE', 'POSHOLD', 'BRAKE', 'THROW', 'AVOID_ADSB', 'GUIDED_NOGPS', 'SMART_RTL', 'FLOWHOLD', 'FOLLOW', 'ZIGZAG', 'SYSTEMID', 'AUTOROTATE', 'AUTO_RTL'])
```





