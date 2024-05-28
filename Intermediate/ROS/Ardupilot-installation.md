# Installing Ardupilot

Get git
```bash
sudo apt-get update
sudo apt-get install git
sudo apt-get install git-gui
```
Clone the ardupilot repo _in your home directory(recommended)_
```bash
git clone https://github.com/ArduPilot/ardupilot.git
```
For ubuntu ardupilot provides you a [script](https://github.com/ArduPilot/ardupilot/blob/master/Tools/environment_install/install-prereqs-ubuntu.sh) for installation (for more info about script file check out [creating and running a acript file](https://www.theserverside.com/blog/Coffee-Talk-Java-News-Stories-and-Opinions/run-Unix-shell-script-Linux-Ubuntu-command-chmod-777-permission-steps))
```bash
cd ardupilot
Tools/environment_install/install-prereqs-ubuntu.sh -y
```
Reload the path (log-out and log-in to make it permanent)
```bash
. ~/.profile
```
for more info you can go through [Setting up the build environment(linux/ubuntu)](https://ardupilot.org/dev/docs/building-setup-linux.html#)

to check the installation execute the following command
```bash
cd ardupilot/ArduCopter && sim_vehicle.py -v copter --console --map -w
```
![](https://github.com/Bhaveshmeghwal21/GIFs/blob/main/gif_summer_camp/Screenshot%20from%202024-05-28%2017-21-41.png)

otherwise 
reinstall it!!

Ardupilot capabilities can be extended with ROS

# ROS with SITL
## Connect ardupilot to ROS 
First create a worksapce 
```bash
mkdir -p ardupilot_ws/src
cd ardupilot_ws
catkin init
cd src
```
Now ROS is ready to use, launch a SITL instance in different terminal 
```bash
sim_vehicle.py -v ArduCopter --console --map
```
(–console to show mavproxy console, –map to have the copter on map)

Now you got an SITL instance launched with TCP and UDP access, you should have some line like:
```bash
"mavproxy.py" "--master" "tcp:127.0.0.1:5760" "--sitl" "127.0.0.1:5501" "--out" "127.0.0.1:14550" "--out" "127.0.0.1:14551" "--map" "--console"
```
Both “–out” refer to UDP connexion create by MAVProxy. We will use UDP access with mavros.

Get back to your ROS terminal. Let’s create a new directory for our launch file.
```bash
mkdir launch
cd launch
```
Let's copy MAVROS default launch file for ardupilot
```bash
roscp mavros apm.launch apm.launch
```

You should have a new file in your directory called “apm.launch”. “roscp” command is just a helper to call system command on ROS package. Open it with your favorite editor, mine is gedit.
```bash
gedit apm.launch
```
You just have to change the first line ``` <arg name="fcu_url" default="/dev/ttyACM0:57600" />```
In my case it was something like this
```launch
<launch>
	<!-- vim: set ft=xml noet : -->
	<!-- example launch script for ArduPilot based FCU's -->

	<arg name="fcu_url" default="udp://127.0.0.1:14550@" />
	<arg name="gcs_url" default="" />
	<arg name="tgt_system" default="1" />
	<arg name="tgt_component" default="1" />
	<arg name="log_output" default="screen" />
	<arg name="fcu_protocol" default="v2.0" />
	<arg name="respawn_mavros" default="false" />

	<include file="$(find mavros)/launch/node.launch">
		<arg name="pluginlists_yaml" value="$(find mavros)/launch/apm_pluginlists.yaml" />
		<arg name="config_yaml" value="$(find mavros)/launch/apm_config.yaml" />

		<arg name="fcu_url" value="$(arg fcu_url)" />
		<arg name="gcs_url" value="$(arg gcs_url)" />
		<arg name="tgt_system" value="$(arg tgt_system)" />
		<arg name="tgt_component" value="$(arg tgt_component)" />
		<arg name="log_output" value="$(arg log_output)" />
		<arg name="fcu_protocol" value="$(arg fcu_protocol)" />
		<arg name="respawn_mavros" value="$(arg respawn_mavros)" />
	</include>
</launch>
```

