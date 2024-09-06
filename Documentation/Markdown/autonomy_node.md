# File: autonomy_node.cpp
## File Author: Bill Johnson
## Documentation Author(s): Andrew Burroughs
## Detailed Description: 
This file handles the autonomous movement of the robot.  It receives information from the logic node about the location of the camera and sets the speeds of the right and left side motors to move the robot to the correct position.  When this node is active, it will override the user input from the joystick for the motor movement.

## Issues:
While the code causes the robot to turn and drive until the robot is less than a meter away from the Aruco marker, this does not square the robot up to the marker.

# Software Documentation
## Global Variables
### **nodeHandle**
This is an instance of the ROS2 pointer and is used to create the ROS2 node.

### **driveLeftSpeedPublisher**
This is a ROS2 publisher of type Float32 that publishes the speed data for the left motors.

### **driveRightSpeedPublisher**
This is a ROS2 publisher of type Float32 that publishes the speed data for the right motors.


## Function Documentation
### **positionCallback**(const messages::msg::ZedPosition::SharedPtr zedPosition)
This function is called when the zedPositionSubscriber receives a message with the topic zed_position.  There are three conditional statements that check the following conditions: if the Aruco is visible and the camera is more than a meter away from the marker, if the Aruco is visible and the camera is less than 2.5 meters and greater than 0 meters, and if the Aruco marker isn’t visible.  The speeds are set by the conditionals and published.
#### Expected Input:
zedPosition – ZedPosition message containing seven float values and one Boolean value
#### Expected Results:
The node will set the speed data and publish the speed data for the motors.



# Change Log:
7/3/2022: Documentation was created

9/30/2022: Markdown file was created by Andrew Burroughs