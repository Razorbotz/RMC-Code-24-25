# File: Automation1.cpp
## Authors: Andrew Burroughs, Bill Johnson
## Documentation Author: Andrew Burroughs
## Detailed Description: 
This file implements some logic for the autonomous movement.  It makes use of an enum to track the state of the robot and adjust the behavior accordingly.  

## Issues:
The logic for most of these states are not fully implemented.

# Software Documentation
## Global Variables
### **enum RobotState**
This is an enum that holds the values LOCATE, GO_TO_DIG_SITE, DIG, HOME, DOCK, and DUMP.  This is used to track the state of the robot and to aid in the flow of the program.

## Function Documentation
### **automate**():
This function implements the logic needed for the robot to run autonomously.  When the robot is in the LOCATE state, the robot turns until the camera can see the Aruco marker, then drives towards it.  When the robot is in the GO_TO_DIG_SITE state, the robot drives forward.  When the robot is in the DIG state, the robot was intended to go through the full mining sequence, though the logic hasn’t been fully implemented.  When the robot is in the DUMP state, it will fully extend, then retract the linear actuator attached to the dump bin.
#### Expected Input
None
#### Expected Results
The robot should perform some movements autonomously and should be able to fully extend and dump the regolith collected.

# Change Log:
7/3/2022: Documentation was created

9/30/2022: Markdown file was created by Andrew Burroughs