Orocos-KDL
==========

Official website: http://www.orocos.org/kdl

Packages for ROS Installation
-----------------------------

.. highlight:: bash

Installation
    + ``sudo apt-get install ros-<distro>-orocos-kdl  # Orocos-KDL main library``
    + ``sudo apt-get install ros-<distro>-kdl-parser  # model file parser``

Link files
    + orocos-kdl
    + kdl_parser

Include files
    + ``kdl/kdl_parser.hpp``  model parser
    + ``kdl/chain.hpp``
    + ``kdl/frames.hpp``  declaration for frames
    + ``kdl/jntarray.hpp``  declaration for joint-state variables
    + ``kdl/chainfksolverXXX_YYY.hpp`` forward kinematics/dynamics solver
    + ``kdl/chainiksolverXXX_YYY.hpp`` inverse kinematics/dynamics solver

Generate Models
---------------

convert .xacro file to .urdf file
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

    rosrun xacro xacro --inorder <xacro_input_file> > <urdf_output_file>

Usage
----

.. highlight:: cpp


Parse Models
~~~~~~~~~~~~

.. code-block:: cpp

    KDL::Tree tree;                              // model tree
    kdl_parser::treeFromFile(urdf_file, tree);   // parse from urdf file

    KDL::Chain chain                             // link chains
    tree.getChain("<start_segment_name>", "<end_segment_name>", tree);

Forward Kinematics/Dynamics
~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: cpp

    KDL::ChainFkSolverXXX *fk_solver;
    fk_solver = new KDL::ChainFkSolverXXX_YYY(chain);

    KDL::JntArray joint_position;
    KDL::Frame end_frame;
    fk_solver->JntToCart(joint_position, end_frame);

Inverse Kinematics/Dynamics
~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: cpp

    KDL::ChainIkSolverXXX *ik_solver;
    ik_solver = new KDL::ChainIkSolverXXX_YYY(chain);

    KDL::JntArray joint_start_position, joint_target_position;
    KDL::Frame target_frame;
    ik_solver->CartToJoint(joint_start_position, target_frame, joint_target_position);
