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

3. Official simulator (optional)

    1. download the software

        Goto https://www.universal-robots.com/download/ and select *Software*, *Offline Simulator*,
        *Linux*, *ursim-<vesrion>*. Then click *Download*.

    #. unzip the downloaded file
    #. install with ::

        ./ursim-<version>/install.h

    #. run the simulator with ::

        ./ursim-<version>/start-ursim.h

    #. the IP address of this "robot" should be `127.0.0.1`

Run
---

+ launch the driver

    .. code-block:: bash

        # Normal mode
        roslaunch ur_modern_driver ur5_bringup.launch robot_ip:=<ROBOT_IP_ADDRESS>

        # ros_control mode
        roslaunch ur_modern_driver ur5_ros_control.launch robot_ip:=<ROBOT_IP_ADDRESS>

+ if you want to switch from ``vel_based_pos_traj_controller`` to ``pos_based_pos_traj_controller``

    .. code-block:: bash

        rosservice call /universal_robot/controller_manager/switch_controller \
            "start_controllers: - 'pos_based_pos_traj_controller' \
             stop_controllers: - 'vel_based_pos_traj_controller' \
             strictness: 1"

+ launch Moveit (optional)

    .. code-block:: bash

        roslaunch ur5_moveit_config ur5_moveit_planning_executing.launch
        roslaunch ur5_moveit_config moveit_rviz.launch config:=true

+ launch Gazebo for simulation (optional)

    .. code-block:: bash

        roslaunch ur_gazebo ur5.launch

Usage
-----

read joint states
^^^^^^^^^^^^^^^^^

+ message type: ``sensor_msg::JointState``
+ topic name: ``joint_states``
+ frequency: about :math:`120 \mathrm{ Hz}`
+ ⚠WARNING⚠: be careful with the joints' names

follow a trajectory
^^^^^^^^^^^^^^^^^^^

+ action type: ``control_msgs::FollowJointTrajectory``
+ server name: ``follow_joint_trajectory``

use build-in ``pos_based_pos_traj_controller`` (ros_control mode)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

+ ⚠NOTE⚠: the topic ``joint_states`` is NOT enabled
+ read joint states

    - message type: ``control_msgs::JointTrajectoryControllerState``
    - topic name: ``pos_based_pos_traj_controller/state``

+ follow trajectory

    - action type: ``control_msgs::FollowJointTrajectory``
    - server name: ``pos_based_pos_traj_controller/follow_joint_trajectory``
    - the velocity field is not used

direct URScript (Advanced) ⚠
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**⚠WARNING⚠**
    USE AT YOUR OWN RISK

+ message type: ``std_msgs::String``
+ topic name: ``ur_driver/URScript``
+ official document:

    - goto https://www.universal-robots.com/download/
    - select *Manuals - user, software and script*, *SW<version>*, *Script manual*
    - click *Download*
