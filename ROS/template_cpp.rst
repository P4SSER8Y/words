Templates for ROS (C++)
=======================

Publisher & Subscriber
----------------------

.msg file 
~~~~~~~~~

::

    Header Header
    string hello_world
    geometry_msgs/PoseWithCovariance pose

Publisher
~~~~~~~~~

.. code-block :: cpp
    :linenos:

    typedef Foobar MsgType;

    ros::Publisher pub;

    void init()
    {
      // ros::NodeHandle node;
      pub = node.advertise<MsgType>("topic_name", buffer_size);
    }

    void publish()
    {
      MsgType msg;
      // fill msg
      pub.publish(msg);
    }

Subscriber
~~~~~~~~~~

.. code-block :: cpp
    :linenos:

    typedef Foobar MsgType;

    ros::Subscriber sub;

    void init()
    {
      // ros::NodeHandle node;
      sub = node.subscribe("topic_name", buffer_size, callback);
      // ros.spin();
    }

    void callback(const MsgType::ConstPtr& msg)
    {
      // do something with received msg
    }



Server & Client
---------------

.srv file
~~~~~~~~~

::

    string name
    ---
    string greet

Server
~~~~~~

.. code-block :: cpp
    :linenos:

    typedef Foobar SrvType;

    ros::ServiceServer server;

    void init()
    {
      // ros::NodeHandle node;
      server = node.advertiseService("server_name", func);
    }

    bool func(SrvType::Request  &request,
              SrvType::Response &response)
    {
      // Generate response with request
      return true;   // if success
      return false;  // if faile
    }


Client
~~~~~~

.. code-block :: cpp
    :linenos:

    typedef Foobar SrvType;

    ros::ServiceClient client;

    // ros::NodeHandle node;
    client = node.serviceClient<SrvType>("server_name");

    SrvType srv;
    // fill srv.request
    if (client.call(srv))
    {
      // successed with response placed in srv.response
    }
    else
    {
      // failed
    }


actionlib
---------

For more information, see http://wiki.ros.org/actionlib_tutorials/Tutorials/SimpleActionClient\ .

Client
~~~~~~

.. code-block :: cpp
    :linenos:

    #include <actionlib/client/simple_action_client.h>
    #include <foobar/foobarAction.h>

    typedef Foobar ActionType;
    // ... ActionGoalType, ActionStateType

    auto ac = new actionlib::SimpleActionClient<ActionType>("action_name", true);
    ac.waitForServer(timeout);  // or use ac.waitForServer(); to wait forever

    ActionGoalType goal;
    // fill in goal
    ac.sendGoal(goal);
    
