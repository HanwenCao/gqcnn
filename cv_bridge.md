### Solution from [here](https://github.com/pulver22/gym-gazebo/wiki/ERROR:-Cv_bridge-for-Python3)
* Install few dependencies: `python-catkin-tools` is needed for catkin tool
`python3-dev` and `python3-catkin-pkg-modules` is needed to build cv_bridge
`python3-numpy` and `python3-yaml` is cv_bridge dependencies
`ros-kinetic-cv-bridge` is needed to install a lot of cv_bridge deps. Probaply you already have it installed.
```
sudo apt-get install python-catkin-tools python3-dev python3-catkin-pkg-modules python3-numpy python3-yaml ros-kinetic-cv-bridge
```

* Create catkin workspace
```
mkdir -p catkin_workspace/src
cd catkin_workspace
catkin init
```
* Instruct catkin to set cmake variables
```
catkin config -DPYTHON_EXECUTABLE=/usr/bin/python3 -DPYTHON_INCLUDE_DIR=/usr/include/python3.5m -DPYTHON_LIBRARY=/usr/lib/x86_64-linux-gnu/libpython3.5m.so
```
* Instruct catkin to install built packages into install place. It is $CATKIN_WORKSPACE/install folder
```
catkin config --install
```
* Clone cv_bridge src
```
git clone https://github.com/ros-perception/vision_opencv.git src/vision_opencv
```
* Find version of cv_bridge in your repository
```
apt-cache show ros-kinetic-cv-bridge | grep Version
    Version: 1.12.8-0xenial-20180416-143935-0800
```
* Checkout right version in git repo. In our case it is 1.12.8
```
cd src/vision_opencv/
git checkout 1.12.8
cd ../../
```
* Build
```
catkin build cv_bridge
```
* Extend environment with new package
```
source install/setup.bash --extend
```

### Test
```
$ python3

Python 3.5.2 (default, Nov 23 2017, 16:37:01) 
[GCC 5.4.0 20160609] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from cv_bridge.boost.cv_bridge_boost import getCvType
>>> 
```

### Use in another workspace

* Step1. create a separate workspace containing only cv_bridge as the above instruction
* Step2. source this ws using source install/setup.bash --extend as the above instruction
* Step3. source the main ws using source devel/setup.bash --extend
