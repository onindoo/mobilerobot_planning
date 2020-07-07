# Grid Based Astar Planner for Mobile Robots 


> ## Description
> - Rosnode that find feasible astar path from current position to target position using [SBPL](http://www.ros.org/wiki/sbpl) Library . Target position is published into topic /clicked_point from rviz and the path produced is also visualized in rviz .

> ## Visual
![](images/udacity_capstone.gif)

> ## Setup
> - ####To run this project


```shell
        $roslaunch turtlebot3_gazebo turtlebot3_world.launch 
```
```shell
        $roslaunch turtlebot3_navigation turtlebot3_navigation.launch
```
```shell
        $rosrun planner rosnode_test
```

> ## OverView
> - There are three main classes in this project . SBPLinterface which is an interface class that extends thr SBPL library . ROSNode class which creates all ROS related work like subscribing into a topic or publishing into a topic . Planner Class which creates  object of the SBPLinterface Class and ROSNode class. The main node creates an object of Planner Class . First Planner Class takes all information of the enviroment from ROSNode Class which subscribe to topic `/move_base/global_costmap/costmap` and then Planner Class initialises the enviroment using the SBPLinterface object by calling `setEnvironmentValue()` member function of SBPLinterface Class. The ROSNode Class is also subscribed to  topic `/amcl_poses` , which updates the member variables `currentX_` , `currentY_` and `currentTheta_` which indicates the current position of the Robot . ROSNode class is also subscribed to `/clicked_point` . Whenever a point is published into the topic `/clicked_point` , member variables `targetX_` , `targetY_` and `targetTheta_` gets updated and a boolean variable indicating a new target position becomes true . The Planner Class will plan whenever a new target position is available by always monitoring that boolean member variable of the ROSNode Class . Planner Class will now call member function `planxythetalat()` of SBPLinterface Class with help SBPLinterface Class object and will publish the path into the topic `/astar` with help of ROSNode Class object . This path can be visualized in rviz by subscribing into topic `/astar`.

> ## Rubric Points
>
> - The project uses Object Oriented Programming techniques. The classes SBPL , ROSNode and Planner are declared in SBPLinterface.h , ROS_node.h and planner.h respectively and defined in SBPLinterface.cpp, ROS_node.cpp and planner.cpp respectively.
> - In ROS_node.h ,SBPLinterface.h and Planner.h ,class member has been defined in appropriate access specifier.
> - In ROS_node.cpp ROSNode constructor line no. 3 member variable `ros::NodeHandle nh_` is initialized using initialization lists. 
> - All information related to ROS is in class ROSNode. And all thing related for SBPL library is in SBPLinterface class . Hence encalsulation.
> - In SBPLinterface.cpp member function planxythetalat() line no 25  use pass by reference also member function setEnvironmentValue() line no 166 uses pass by reference.
> - In SBPLinterface.cpp , destructor ~SBPL() line no. 17 dynamic allocated memory is deallocated.
> - In SBPLinterface.cpp ,  line no 54  uses unique_ptr to create instance of SBPLPlanner . Also in planner.h line no. 8 and 9 declares two shared_ptr for classes SBPLinterface and ROSNode . It is defined in line no 5 snd 7 in planner.cpp .
> - In test_ros_node.cpp line no 12 a thread is created .
