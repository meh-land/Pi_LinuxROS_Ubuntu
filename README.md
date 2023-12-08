# Pi_LinuxROS_Ubuntu
This repository contains step-by-step instructions to set an Ubuntu Server 20.04 LTS running ROS 1 Noetic on the Raspberry Pi 4.


## RPI Imager
1. Choose Ubuntu Server 20.04 LTS.
2. DO NOT SET A DEFAULT WIFI NETWORK.
3. Set Hostname as raspberrypi.
4. Enable SSH - Use password authentication.
5. Username: pi - Password: 123
6. Set locale settings - Time zone: Africa/Cairo - Keyboard layout: us


## PuTTY - Serial Communication with Pi
1. Choose 'Serial' as the connection type.
2. In serial line, write COMx - Check the device manager to see which COM port you are using.
3. Speed: 115200.
4. Press `Open` and power up the Pi.


## Pi - on boot (MUST DO)
1. Disable unattended updates completely. 
  ```
  sudo apt remove unattended-upgrades
  ```
2. Connect an Ethernet cable to the Pi to have access to the internet.
3. Install nmcli to connect to wifi. 
  ```
  sudo apt install network-manager
  ```
4. Run these commands to connect to ESP network.
  ```
  nmcli radio wifi
  sudo nmcli dev wifi connect ourESP password ourESP123
  ```
5. Update and upgrade all packages.
   ```
   sudo apt update && sudo apt upgrade -y
   ```


## Pi - SSH Through PC
1. Since the Pi is connected on the ESP network, make sure your PC is also connected to it.
2. Open cmd on Windows or terminal on Linux.
3. Enter the following command:
  ```
  ssh pi@raspberrypi
  ```
4. You will be prompted to enter the password.
5. Voila!


## Pi - ROS 1 Noetic Setup (METHOD 1)
1. Setup the Pi to accept software from packages.ros.org
   ```
   sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
   ```
2. Set up your keys. Make sure `curl` is installed.
   ```
   curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
   ```
3. Run:
   ```
   sudo apt update
   ```
4. Install ROS-Desktop-Full.
   ```
   sudo apt install ros-noetic-desktop-full
   ```
5. Run this script to use ROS.
   ```
   source /opt/ros/noetic/setup.bash
   ```
6. OPTIONAL: Source the previous script on startup using `.bashrc`.
   ```
   echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
   source ~/.bashrc
   ```


## Pi - ROS 1 Noetic Setup (METHOD 2)
1. Run this single line command to install ROS 1 Noetic *BRUH!*
   ```
   wget -c https://raw.githubusercontent.com/qboticslabs/ros_install_noetic/master/ros_install_noetic.sh && chmod +x ./ros_install_noetic.sh && ./ros_install_noetic.sh
   ```
2. Run this single line command to uninstall ROS 1 Noetic.
   ```
   wget -c https://raw.githubusercontent.com/qboticslabs/ros_install_noetic/master/ros_uninstall_noetic.sh && chmod +x ./ros_uninstall_noetic.sh && ./ros_uninstall_noetic.sh
   ```
