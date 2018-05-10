Orocos-KDL
==========

Orocos-KDL 机器人运动学/动力学计算库。

官方主页： http://www.orocos.org/kdl

ROS 安装 & 使用
---------------

.. highlight:: bash

指令
    + ``sudo apt-get install ros-<distro>-orocos-kdl  # Orocos-KDL 主库``
    + ``sudo apt-get install ros-<distro>-kdl-parser  # 模型解释库``

链接文件
    + orocos-kdl
    + kdl_parser

引用文件
    + ``kdl/kdl_parser.hpp``  模型解释库
    + ``kdl/chain.hpp``  运动链定义
    + ``kdl/frames.hpp``  坐标框定义
    + ``kdl/jntarray.hpp``  关节空间坐标定义
    + ``kdl/chainfksolverXXX_YYY.hpp`` 正向运动学/动力学解算
    + ``kdl/chainiksolverXXX_YYY.hpp`` 逆向运动学/动力学解算

生成模型
--------

.xacro 转换为 urdf 文件
~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

    rosrun xacro xacro --inorder <xacro_input_file> > <urdf_output_file>

用例
----

.. highlight:: cpp


解释模型
~~~~~~~~

.. code-block:: cpp

    KDL::Tree tree;                              // 模型描述树
    kdl_parser::treeFromFile(urdf_file, tree);   // 从文件中解释模型

    KDL::Chain chain                             // 运动链
    tree.getChain("<start_segment_name>", "<end_segment_name>", tree);  // 获取运动链

正向运动学
~~~~~~~~~~

.. code-block:: cpp

    KDL::ChainFkSolverXXX *fk_solver;
    fk_solver = new KDL::ChainFkSolverXXX_YYY(chain);

    KDL::JntArray joint_position;
    KDL::Frame end_frame;
    fk_solver->JntToCart(joint_position, end_frame);

逆向运动学
~~~~~~~~~~

.. code-block:: cpp

    KDL::ChainIkSolverXXX *ik_solver;
    ik_solver = new KDL::ChainIkSolverXXX_YYY(chain);

    KDL::JntArray joint_start_position, joint_target_position;
    KDL::Frame target_frame;
    ik_solver->CartToJoint(joint_start_position, target_frame, joint_target_position);
