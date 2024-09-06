# File: power_distribution_panel_node.cpp
## Author: Bill Johnson
## Documentation Author: Andrew Burroughs
## Detailed Description: 
The power_distribution_panel_node.cpp file is responsible for publishing values found in PowerDistributionPanel.cpp. This class queries the PDP and packages this information into one topic. The purpose of this class is to allow the information found in the PowerDistributionPanel.cpp to be published for other ROS2 nodes to read.

## Issues:
None

# Software Documentation
## Global Variables
None

## Function Documentation
### **int main**(int argc, char **argv):
This is the main function for the file, and the only function defined in this file.
The main function initializes the ROS2 node by calling the `rclcpp::init` function and creating a node handle object. It then creates a publisher object that publishes messages of the type `messages::msg::Power` to the "power" topic with a queue size of 1. The `messages::msg::Power` message type is defined in the "power.hpp" header file and contains fields for the volatage and current readings from the PDP.
The code intializes a socket to read data from the CAN bus. It then creates an instance of the `PowerDistributionPanel` class. This class contains functions to parse the CAN messages and extract voltage and current data from the PDP.
The main loop of the node continuously reads data from the CAN bus using the `read` function. If this function returns -1, the loop continues without updating the `pdp` object. Otherwise, the received CAN message is parsed using the `pdp.parseFrame` function. After parsing, the volate and current readings from the PDP are assigned to the corresponding fields in the `power` message.
The node then check if at least 250 milliseconds have passed since the last message was published. If so, the `power` message is published to the "power" topic using the `publisher->publish` function. The loop then repeats.
The node handles any pending callbacks using the `rclcpp::spin_some` function. The loop continues until the `rclcpp::ok` function returns `false` indicating that the ROS2 node was shutdown.


# Change Log:
7/3/2022: Documentation was created

3/4/2023: Documentation completed