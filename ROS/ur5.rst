Universal Robot 5
=================

UR5 robot arm.

**NOTE** 
    This note is for ROS Kinetic Kame.

Installation
------------

1. create and enter a workspace
    .. code-block:: bash

        pushd
        mkdir -p ur_ws/src
        cd ur_ws
        catkin_make
        popd

2. clone drivers
    .. code-block:: bash

        pushd
        cd ur_ws/src
        # this is the main drivers, including driver and related resource
        git clone https://github.com/ros-industrial/universal_robot.git
        cd universal_robot
        git checkout kinetic-devel
        popd

        # this is a better driver
        # I adapted it to kinetic
        pushd
        cd ur_ws/src
        git clone https://github.com/P4SSER8Y/ur_modern_driver
        popd

        # build
        pushd
        cd ur_ws
        catkin_make
        popd
