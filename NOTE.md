## installation
.uw move command to home directory error
    * check the folder is somehow already there and delete it

## Operation
```
catkin_make_isolated --install
source install_isolated/setup.bash
roslaunch parse:=true → throw an error is correct
roslaunch parse:=false → running the simulator
```

## Modification
### controller
* comment: 
    * patrol_pid_scence: controller for ASV to navigate as per the pre-programming
    * pid_control, control_vel, heading_control: lin, angular velocity control and motor L,R controller
* new
    * urdf.xacro includes “planar_move_plugin” for cmd_vel

* Controller revisit
    * controller revisit
    * disable planar move_plugin
    * enable diff_vel_control
    * enable heading and pid control
    * There was no D control for lin and ang vel

### tf: 
* comment: 
    * odom_relay: node to publish global /odom topic
* new
    * urdf.xacro includes “planar_move_plugin” for odom, base_link
* namespace
    * xacro: pass argument via xacro file and xacro file has argument and parameter such that robot namespace can be used ${robotName}

### launch file naming
* test
    * diffboat_scenario_test for all postfix

### sensor
* laser remove
    * boat_subdivided_validated.xacro: comment laser sensor as there was a global /scan topic


### environmental setup
* water HECRAS current
* wind current
    * No such file or directory: '/home/mingi/usv_sim_ws/install_isolated/share/wind_current/diluvio/p0.8.csv'
    * download data and move to installed_isolated folder

## Start simulation
### external disturbances
* water current
```
rosrun water_current water_HECRAS.py /home/mingi/usv_sim_ws/install_isolated/share/water_current/maps/HECRAS/diluvio1.yaml
```



### Run obstacle avoidance algorithm
```
roslaunch obstacle_avoidance_ros_pkg master_controller.launch obstacle_total:=3 case:=4 open_rviz:=true master_visualization:=true avoidance_algo:=MOA open_stage:=false adaptive_avoidance:=true use_logging:=true
```

### Execute
```
rosservice call /gazebo/unpause_physics "{}"
```