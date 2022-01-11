## Operation
```
catkin_make_isolated
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