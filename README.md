# About
This is fork from [VINS-Fusion-gpu](https://github.com/pjrambo/VINS-Fusion-gpu) for opencv 4 version (and some fix).
VINS-Fusion-gpu is a version of [VINS-Fusion](https://github.com/HKUST-Aerial-Robotics/VINS-Fusion) with GPU acceleration.


# OpenCV bridge
This is require ROS and OpenCV bridge for OpenCV 4.

```
cd ~/catkin_ws/src
git clone https://github.com/ros-perception/vision_opencv
```

In CMakeLists.txt change python version (if necessary):
```
nano vision_opencv/cv_bridge/CMakeLists.txt
```
```
find_package(Boost REQUIRED python37) -> find_package(Boost REQUIRED python3)
```

In module.hpp add define NUMPY_IMPORT_ARRAY_RETVAL:
```
nano vision_opencv/cv_bridge/src/module.hpp
```
```cpp
#include <numpy/ndarrayobject.h>
#define NUMPY_IMPORT_ARRAY_RETVAL NULL
```

Build OpenCV bridge:
```
cd ~/catkin_ws
catkin_make
```


# Build
Build is same as VINS-Fusion-gpu and VINS-Fusion.

```
sudo apt-get install ros-melodic-tf ros-melodic-image-transport
```

Clone the repository and catkin_make:
```
cd ~/catkin_ws/src
git clone https://github.com/IOdissey/VINS-Fusion-GPU.git
cd ../
catkin_make
source ~/catkin_ws/devel/setup.bash
```


# Usage
In the config file, there are two parameters for gpu acceleration.

GPU for GoodFeaturesToTrack (0 - off, 1 - on) 
```
use_gpu: 1
```

GPU for OpticalFlowPyrLK (0 - off, 1 - on) 
```
use_gpu_acc_flow: 1
```

If your GPU resources is limitted or you want to use GPU for other computaion. You can set
```
use_gpu: 1
use_gpu_acc_flow: 0
```

If your other application do not require much GPU resources (recommanded)
```
use_gpu: 1
use_gpu_acc_flow: 1
```

There are two parameters for config OpticalFlowPyrLK (pyramid level and window size):
```
lk_n = 3
lk_size = 21
```
