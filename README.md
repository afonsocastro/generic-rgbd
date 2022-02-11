# generic-rgbd

## Table of Contents

1. [Configuration](#configuration)
1. [Installation](#installation)
2. [Simple RGB-D object tracking](#simple-rgb-d-object-tracking)
3. [Sending TF (via socket communication) of wood-block RGB-D tracking](#sending-tf-via-socket-communication-of-wood-block-rgb-d-tracking)

## Configuration
This repository was built to work with:
* Intel RealSense D435 RGB-D camera
* Ubuntu 20.04.3 LTS 64bits

## Installation
1. [Creating workspace with source](#creating-workspace-with-source)
2. [Including this repo and building](#including-this-repo-and-building)
3. [Installing librealsense 3rd party](#installing-librealsense-3rd-party)

### Creating workspace with source
First create a workspace that will contain all ViSP source, build, data set and optional 3rd parties. This workspace is here set to $HOME/visp-ws folder, but it could be set to any other location.

In a terminal, run:

```
echo "export VISP_WS=$HOME/visp-ws" >> ~/.bashrc
source ~/.bashrc
mkdir -p $VISP_WS
```

Then, install the standard (recommended) 3rd parties:
```
sudo apt-get install libopencv-dev libx11-dev liblapack-dev libeigen3-dev libv4l-dev libzbar-dev libpthread-stubs0-dev libjpeg-dev libpng-dev libdc1394-22-dev
```

Clone the source code:
```
cd $VISP_WS
git clone https://github.com/lagadic/visp.git
```

### Including this repo and building
Change the generic-rgbd folder to this repository:
```
cd $VISP_WS/visp/tutorial/tracking/model-based
rm -rf generic-rgbd
git clone https://github.com/afonsocastro/generic-rgbd.git
```

Create a build folder and build ViSP: 
```
mkdir -p $VISP_WS/visp-build
cd $VISP_WS/visp-build
cmake ../visp
make -j4
``` 

Set VISP_DIR environment variable: 
```
echo "export VISP_DIR=$VISP_WS/visp-build" >> ~/.bashrc
source ~/.bashrc
```

Copy *learning* folder to visp-build:
```
cp -a ~/visp-ws/visp/tutorial/tracking/model-based/generic-rgbd/learning  ~/visp-ws/visp-build/tutorial/tracking/model-based/generic-rgbd/
```

### Installing librealsense 3rd party
If you have an Intel RealSense Depth camera (SR300 or D400 series), you may install librealsense 2.x in order to use vpRealSense2 class.
1. Get librealsense from github: 
```
cd $VISP_WS
git clone https://github.com/IntelRealSense/librealsense.git
cd librealsense
```

2. Ensure no Intel RealSense cameras are plugged in.
3. Install udev rules located in librealsense source directory:
```
sudo cp config/99-realsense-libusb.rules /etc/udev/rules.d/
sudo udevadm control --reload-rules && udevadm trigger
```

4. Install the packages required for librealsense build:
```
sudo apt-get install libssl-dev libusb-1.0-0-dev pkg-config libgtk-3-dev
```

5. Install distribution-specific packages:
```
sudo apt-get install libglfw3-dev libgl1-mesa-dev libglu1-mesa-dev
```

6. Build and install librealsense:
```
mkdir build
cd build
cmake .. -DBUILD_EXAMPLES=ON -DCMAKE_BUILD_TYPE=Release
make -j4
sudo make install
```

## Simple RGB-D object tracking

[under construction]

## Sending TF (via socket communication) of wood-block RGB-D tracking

[under construction]