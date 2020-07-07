# Table Docking with Node Diagnostics
1) The first stage begins with an omni-directional robot parked in front of a table. The four legs of the table are visible to the Lidar sensor at the centre of the robot.
2) In the second stage, the robot will then find its way to go underneath the table, and it will align and center itself within 4 legs of the table as shown in the picture attached. Additionally the robot will response to the movement of the table accordingly.

### Prerequisites

1) Install ROS Kinetic with ubuntu 16.04.

### Instructions

1) create a workspace <br />
$ mkdir -p ~/catkin_ws/src <br />
$ cd ~/catkin_ws/src <br />
$ catkin_init_workspace <br />
$ cd .. <br />
$ catkin_make <br />
   
2) Clone the project and launch <br />
$ cd ~/catkin_ws/src <br />
$ git clone https://github.com/rvipin17/robo.git <br />
$ cd .. <br />
$ catkin_make <br />
$ source ~/catkin_ws/devel/setup.bash <br />
$ roslaunch robo robo.launch <br />

3) Now you will see robot getting inside the robot. Please change the table position, the robot will respond accordingly. 

## Diagnostics Monitoring

A monitoring system for tracking the node alive status and report error under /monitoring topic. 

### Node monitor

A Node monitor that pings every node from the list of monitoring nodes (from the parameter file). 

**Monitored Values:**

|     values      | unit  |          Comment                   |
|-----------------|-------|------------------------------------|
|     isAvailable    |       |         True, if the node is registered to the master                          |

**Warning/Errors:**

* Error if, 
     * Node is not available

**Parameters:**


	frequency: 1					# Frequency at which diagnostics updates node errors
	filter_type: 1                                  # 0 (default: monitors all nodes registered to ros) or 
                                                      1 (only monitor nodes provided in the nodes param) or
                                                      2 (monitor all registered nodes except for the nodes in the param)
    nodes: [node_name]                              # List of nodes to be monitored or blacklisted based on filter type
