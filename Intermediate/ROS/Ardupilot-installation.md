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
For ubuntu ardupilot provides you a [script](https://github.com/ArduPilot/ardupilot/blob/master/Tools/environment_install/install-prereqs-ubuntu.sh) for installation (for more info about acript file check out [creating and running a acript file](https://www.theserverside.com/blog/Coffee-Talk-Java-News-Stories-and-Opinions/run-Unix-shell-script-Linux-Ubuntu-command-chmod-777-permission-steps))
```bash
cd ardupilot
Tools/environment_install/install-prereqs-ubuntu.sh -y
```
Reload the path (log-out and log-in to make it permanent)
```bash
. ~/.profile
```
for more info you can go through [Setting up the build environment(linux/ubuntu)](https://ardupilot.org/dev/docs/building-setup-linux.html#)

