# File: zed_node.cpp
## Author: Andrew Burroughs
## Detailed Description: 
This file captures images from the camera.  It is not currently active on the new robot.

## Issues:
This node currently is not active or complete, has no method to publish the images, and is incomplete.  Recommend using as a starting point for extensive modifications or scrapping entirely.

# Software Documentation
## Global Variables
N/A

## Function Documentation
### **Main**(int argc, int argv):
This function is called when the node is created.  It creates a shared ROS2 node with the name zed, publishes the message “Starting ZED node” to the console, and initializes the camera with the given parameters.  The camera will begin to capture images from the camera.
#### Expected Input:
N/A
#### Expected Results
N/A


# Change Log:
7/3/2022: Documentation was created

8/3/2022: Description and issues added by Andrew Burroughs

9/30/2022: Markdown file was created by Andrew Burroughs