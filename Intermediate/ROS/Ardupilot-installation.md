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

### Update Mavrproxy and pymavlink
```bash
sudo pip install --upgrade pymavlink MAVProxy
```

Ardupilot capabilities can be extended with ROS


# Installing Mavros

### What is Mavros?
[Mavros](http://wiki.ros.org/mavros) is a ROS package that can convert between ROS topics and MAVLink messages allowing ArduPilot vehicles to communicate with ROS. [The MAVROS code can be found here.](https://github.com/mavlink/mavros/tree/master/mavros)

### What is MAVLink??
MAVLink is a very lightweight messaging protocol for communicating with drones (and between onboard drone components). _(for more info visit [mavlink](https://mavlink.io/en/))_

Now we will be going through the binary installation only
```bash
sudo apt-get install ros-kinetic-mavros ros-noetic-mavros-extras
```
then install GeographicLib datasets by running ```install_geographiclib_datasets.sh``` script
```bash
wget https://raw.githubusercontent.com/mavlink/mavros/master/mavros/scripts/install_geographiclib_datasets.sh
chmod a+x install_geographiclib_datasets.sh
./install_geographiclib_datasets.sh
```
for further info and for source installation visit [mavros-installation](https://github.com/mavlink/mavros/tree/master/mavros#installation##Sourceinstallation)

**Tip** _Prefer binary installation for convinience and source installation for customization for more info ckeck out [Binary installation vs Source installation](https://www.linux.com/training-tutorials/thoughts-package-managers-source-vs-binary/)_


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
to check type
```bash
roslaunch apm.launch
```
You should see some verbose from MAVROS that read its configuration and some line that indicate a connexion without any error:
```bash
[INFO] [1716899013.356771299]: FCU URL: udp://127.0.0.1:14550@
[INFO] [1716899013.360145095]: udp0: Bind address: 127.0.0.1:14550
[INFO] [1716899013.360324164]: GCS bridge disabled
[INFO] [1716899013.424645942]: Plugin 3dr_radio loaded
[INFO] [1716899013.426759564]: Plugin 3dr_radio initialized
[INFO] [1716899013.426815974]: Plugin actuator_control blacklisted
[INFO] [1716899013.468419183]: Plugin adsb loaded
[INFO] [1716899013.471952305]: Plugin adsb initialized
[INFO] [1716899013.471988582]: Plugin altitude blacklisted
[INFO] [1716899013.472138366]: Plugin cam_imu_sync loaded
[INFO] [1716899013.472740631]: Plugin cam_imu_sync initialized
```
if you encounter an error then make sure your directory is ardupilot_ws/src/launch and you have installed mavros properlly

Now, The connection was done !!!
Let use RQT to how ArduPilot information are shown in ROS. Normally, MAVROS will do most of the translation MAVLink <–> ROS open another terminal and launch RQT with
```bash
rqt
```
go to plugins/ topics /topics monitor TADAM!!!!!! You see all the topics that mavros has to create from ArduPilot information, click on the box to see the current value. You could see in plugins/robot tools/ runtime monitor that everything is ok! _(You can also type rostopic list in other terminal )_

Let’s try to change mode with mavros: go to plugins / services/ services caller set service to /mavros/set_mode set custom_mode to ‘GUIDED’ and click the call button The response should be true, you can look on /mavros/state topic that the mode is now GUIDED. it should be the same in you MAVProxy console.

Now, you know the base of ROS usage with ArduPilot! ROS got plenty others features that you can use like plotting, 3d visualisation, etc.



# Installing Ardupilot Gazebo Plugin
For Gazebo 11
```bash
sudo apt-get install libgazeboX-dev
```
```bash
git clone https://github.com/khancyr/ardupilot_gazebo
cd ardupilot_gazebo
mkdir build
cd build
cmake ..
make -j4
sudo make install
```
```bash
echo 'source /usr/share/gazebo/setup.sh' >> ~/.bashrc
```
Set Path of Gazebo Models (Adapt the path to where to clone the repo)(if you have cloned the repo in home directory then no need to change the command
```bash
echo 'export GAZEBO_MODEL_PATH=~/ardupilot_gazebo/models' >> ~/.bashrc
```
Set Path of Gazebo Worlds (Adapt the path to where to clone the repo)
```bash
echo 'export GAZEBO_RESOURCE_PATH=~/ardupilot_gazebo/worlds:${GAZEBO_RESOURCE_PATH}' >> ~/.bashrc
```
```bash
source ~/.bashrc
```
**Tip** _You can also create a script file so that you won't have to type every command_
DONE!!!
### Test installation 
Launch a SITL-Ardupilot instance in 1st Terminal
```bash
sudo pip install --upgrade pymavlink MAVProxy
```
Open a second Terminal and launch Gazebo running ardupilot_gazebo plugin
```bash
gazebo --verbose worlds/iris_arducopter_runway.world
```


# Gazebo-ROS plugin (roscam)
This contains the ROS integrated custom models and .world files for Gazebo
```bash
# Source ROS
source /opt/ros/noetic/setup.bash
```
Clone custom gazebo ros-package 
```bash
cd ~/
git clone https://github.com/r0ch1n/ardupilot_gazebo_roscam
```
```bash
cd ardupilot_gazebo_roscam
catkin init
```
```bash
cd src
catkin_create_pkg ardupilot_gazebo
cd ..
catkin build
```
Add custom models adn plugins to gazebo
```bash
export GAZEBO_MODEL_PATH=~/ardupilot_gazebo/models:$GAZEBO_MODEL_PATH
export GAZEBO_MODEL_PATH=~/ardupilot_gazebo_roscam/src/ardupilot_gazebo/models:$GAZEBO_MODEL_PATH
export GAZEBO_PLUGIN_PATH=/usr/lib/x86_64-linux-gnu/gazebo-9/plugins:$GAZEBO_PLUGIN_PATH 
export GAZEBO_PLUGIN_PATH=/opt/ros/melodic/lib:$GAZEBO_PLUGIN_PATH
```
### Test installation
```bash
source ~/ardupilot_gazebo_roscam/devel/setup.bash
roslaunch ardupilot_gazebo iris_with_roscam.launch
```
# Run it all
## Gazebo-ROS
Open one terminal and launch ROS integrated gazebo
```bash
#Make sure you have all the right environment, if you are not sure run the following first

source /opt/ros/noetic/setup.bash

export GAZEBO_MODEL_PATH=~/ardupilot_gazebo/models:$GAZEBO_MODEL_PATH
export GAZEBO_MODEL_PATH=~/ardupilot_gazebo_roscam/src/ardupilot_gazebo/models:$GAZEBO_MODEL_PATH
export GAZEBO_PLUGIN_PATH=/usr/lib/x86_64-linux-gnu/gazebo-9/plugins:$GAZEBO_PLUGIN_PATH 
export GAZEBO_PLUGIN_PATH=/opt/ros/melodic/lib:$GAZEBO_PLUGIN_PATH

#Launch ROS integrated Gazebo

source ~/ardupilot_gazebo_roscam/devel/setup.bash

roslaunch ardupilot_gazebo iris_with_roscam.launch
```
## Launch SITL Ardupilot
Open second terminal and launch SITL Ardupilot
```
cd ~/ardupilot/ArduCopter

sim_vehicle.py -f gazebo-iris --console --map
```

## Launch MAVROS
```bash
cd ~/ardupilot_ws/src/launch && roslaunch apm.launch
```


![](https://github.com/yanhwee/ardupilot-gazebo-ros-guide/blob/master/sitl-architecture.svg)



