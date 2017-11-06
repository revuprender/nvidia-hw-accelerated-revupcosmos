# Credits
This repo is based on pigiuz's original code for the older g2 Nvidia GRID (Cloud Graphics) AWS Ec2 instances. Shout out to pigiuz for his original demo using the g2 instances located here: https://github.com/plumbee/nvidia-hw-accelerated-box AWESOME DEMO! Mad Prop points pigiuz! ;-)

Cloned pigiuz repo November 6, 2017 to support g3 instances with corrosponding (latest) NVIDIA Driver and related CUDA software in order to support the newer Tesla M60 GRID GPU instances

# Before you start
This is intended to be a **demo** setup to run hardware accelerated content on AWS g3 (Nvidia Tesla M60) GPU Hardware accelerated instances https://aws.amazon.com/blogs/aws/new-next-generation-gpu-powered-ec2-instances-g3/

# Requirements
These scripts must be run on a M60 instances running Ubuntu 16.04 (HVM).

# What is included?
Among the other packages these scripts will install
- nvidia drivers v384.81 http://www.nvidia.com/download/driverResults.aspx/124722/en-us
- VirtualGL v2.5.2 http://www.virtualgl.org/
- TurboVNC http://www.turbovnc.org/
- docker https://www.docker.com/
- nvidia-docker https://github.com/NVIDIA/nvidia-docker
- nvidia-docker-compose https://github.com/eywalker/nvidia-docker-compose
- a barebone Mate desktop https://mate-desktop.org/

# Installation
SSH into your EC2 box, once in just run the following
```bash
git clone https://github.com/rybruscoe/revup-nvidia-gpu-renderbox-linux
cd revup-nvidia-gpu-renderbox-linux
sudo su
source setup.sh
```
Keep in mind that:
- The installation will reboot the machine once done.
- At the startup the VNC server will start on DISPLAY :1.

# Future Proofing (to support latest Nvidia GRID GPU hardware)
Find updated NVIDIA-Linux-x86_64-*.run driver direct download URL
Simply update line #8 in the root_setup.sh file to reflect the latest Nvidia driver .run URL download
May work for ec2 p2/p3 (Tesla K80/V100) "Deep Learning" GPU Compute instances but requires further R+D investigation/testing

# VNC access
## Password
VNC password is dynamically set to the first 8 characters of your EC2 instance id.
## Display
VNC starts on DISPLAY :1, VirtualGL content will render offscreen and the resulting image will be copied to DISPLAY :1.
## Connection
VNC receives connections from port 5900 + Display.
Given that DISPLAY is :1 the port will be 5901.

# Running HW accelerated content via VirtualGL
VirtualGL provides a 'vglrun' executable which enables (m)any GUI application to access the GPU when needed.
The command below will run glxgears with hardware acceleration
```bash
vglrun glxgears
```

# Running HW accelerated GUI applications using nvidia-docker
Yes, it's possible, check this out
https://github.com/plumbee/nvidia-virtualgl

# Related posts
- https://medium.com/@pigiuz/setting-up-a-hw-accelerated-desktop-on-aws-g2-instances-4b58718a4541#.g80twxf4f
- https://medium.com/@pigiuz/hw-accelerated-gui-apps-on-docker-7fd424fe813e#.e0bhg911w
