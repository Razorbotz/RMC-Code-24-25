# File: communication_node.cpp
## Author: Bill Johnson
## Documentation Author: Andrew Burroughs
Detailed Description: This file receives data from the joystick, talon, camera, and power distribution and then publishes that data to the robot through the rclcpp APIs to the established socket so that the robot moves according to the user's input. The communication file receives the data as ints or floats and then converts that data to hexadecimal before publishing. A lot of the functions in this file take/create a message object and then takes data from other files and appends that data to the message and sends the message to the socket. Other functions determine what the socket address is and sets up the connection with the socket so it can begin sending data to it. The file's main function sets up the socket and publishers by calling these functions and then executes a while loop that continues exectuting until the rclcpp::ok condition is false. There is a nested while loop which takes messages from the joystick and then sends those messages to the socket for the robot to respond to. This file also logs whether or not data has been received as well as what addresses it is trying to connect to during the socket establishment. 

## Issues:


# Software Documentation
## Global Variables
### **std_msgs::msg::Empty empty**
This is a dummy variable used to create publishers with no initial values passed in and also is used to publish nothing when there are no actions taken.

### **bool silentRunning**
This variable determines whether or not the robot is sending data to the client if it is running. There is data that is unimportant that the robot may try to send back to the client so this boolean says whether or not it can.

### **int new_socket**
Socket number.

### **rclcpp::Node::SharedPtr nodeHandle**
This variable is of type rclcpp::Node::SharedPtr and holds a pointer to a ROS2 node. This node provides access to the ROS2 system and acts as a bridge for communication between ROS2 nodes.

### **std::string robotName**
Name of robot.

### **bool broadcast**
If set to true, the file broadcasts data to the socket. 

## Function Documentation
### **void insert**(float value, uint8_t* array):
This function inserts a float value into an array of type uint8_t.
#### Expected Input, Range(s) of Input
The input to this function is a float value and an array of type uint8_t.
#### Expected Outputs / Results, Range
Takes the array and converts the binary representations to hexadecimal.


### **void insert**(int value, uint8_t* array):
This function inserts an int value into an array of type uint8_t.
#### Expected Input, Range(s) of Input
The input to this function is an int value and an array of type uint8_t.
#### Expected Outputs / Results, Range
Takes the array and converts the binary representations to hexadecimal.

### **float parseFloat**(uint8_t* array):
Sets the axisYInteger equal to either itself or a certain value of the array shifted left an arbitrary amount of bits.
#### Expected Input, Range(s) of Input
The input to this function is an array of type uint8_t.
#### Expected Outputs / Results, Range
The axisYInteger converted to float.

### **int parseInt**(uint8_t* array):
Sets the axisYInteger equal to either itself or a certain value of the array shifted left an arbitrary amount of bits.
#### Expected Input, Range(s) of Input
The input to this function is an array of type uint8_t.
#### Expected Outputs / Results, Range
The axisYInteger converted to int.

### **void send**(BinaryMessage message):
Takes a message and converts it to a list of type uint_8 and iterates over all of the bytes, sending that data to the socket.
#### Expected Input, Range(s) of Input
Message message
#### Expected Outputs / Results, Range
Either sends the message to the socket or prints an error if the send was unsuccessful.

### **void send**(std::string messageLabel, const messages::msg::VictorOut::SharedPtr victorOut):
Takes a message from a message label and then adds Device ID, Bus Voltage, Output Current, Output Voltage, and Output Percent values with the respective labels from victorOut to the message object and then sends that message to the send(BinaryMessage message) function above which sends the message to the socket. 
NOTE: We are not currently using victorOut
#### Expected Input, Range(s) of Input
string messageLabel, SharedPtr  victorOut
#### Expected Outputs / Results, Range
Calls the send(BinaryMessage message) function above with the updated message as a parameter.

### **void send**(std::string messageLabel, const messages::msg::TalonOut::SharedPtr talonOut):
Takes a message from a message label and then adds Device ID, Bus Voltage, Output Current, Output Voltage, Output Percent, Temperature, Sensor Postition, Sensor Velocity, closed Loop Error, Integral Accumulator, and Error Derivative values with the respective labels from talonOut to the message object and then sends that message to the send(BinaryMessage message) function above which sends the message to the socket. 
#### Expected Input, Range(s) of Input
string messageLabel, SharedPtr talonOut
#### Expected Outputs / Results, Range
Calls the send(BinaryMessage message) function above with the updated message as a parameter.

### **void send**(std::string messageLabel, const messages::msg::Power::SharedPtr power):
Takes a message from a message label and then adds Voltage, Current 0, Current 1, Current 2, Current 3, Current 4, Current 5, Current 6, Current 7, Current 8, Current 9, Current 10, Current 11, Current 12, Current 13, Current 14, and Current 15 values with the respective labels from talonOut to the message object and then sends that message to the send(BinaryMessage message) function above which sends the message to the socket. 
#### Expected Input, Range(s) of Input
string messageLabel, SharedPtr power
#### Expected Outputs / Results, Range
Calls the send(BinaryMessage message) function above with the updated message as a parameter.

### **void zedPositionCallback**(const messages::msg::ZedPosition::SharedPtr zedPosition):
Creates a message and gives it values X, Y, Z, oX, oY, oZ, oW, and aruco with the respective labels from the zedPostition and then sends that message to the send(BinaryMessage message) function above which sends the message to the socket. 
#### Expected Input, Range(s) of Input
SharedPtr zedPosition
#### Expected Outputs / Results, Range
Calls the send(BinaryMessage message) function above with the updated message as a parameter.

### **void powerCallback**(const messages::msg::Power::SharedPtr power):
Takes the SharedPtr power and sends it to the send(std::string messageLabel, const messages::msg::Power::SharedPtr power) function with the label of "Power".
#### Expected Input, Range(s) of Input
SharedPtr power
#### Expected Outputs / Results, Range
Calls the send(std::string messageLabel, const messages::msg::Power::SharedPtr power) function with the SharedPtr power as the parameter.

### **void talon1Callback**(const messages::msg::TalonOut::SharedPtr talonOut):
Takes the SharedPtr talonOut and sends it to the send(std::string messageLabel, const messages::msg::TalonOut::SharedPtr talonOut) function with the label of "Talon 1".
#### Expected Input, Range(s) of Input
SharedPtr talonOut
#### Expected Outputs / Results, Range
Calls the send(std::string messageLabel, const messages::msg::TalonOut::SharedPtr talonOut) function with the label and SharedPtr talonOut as the parameter. 

### **void talon2Callback**(const messages::msg::TalonOut::SharedPtr talonOut):
Takes the SharedPtr talonOut and sends it to the send(std::string messageLabel, const messages::msg::TalonOut::SharedPtr talonOut) function with the label of "Talon 2".
#### Expected Input, Range(s) of Input
SharedPtr talonOut
#### Expected Outputs / Results, Range
Calls the send(std::string messageLabel, const messages::msg::TalonOut::SharedPtr talonOut) function with the label and SharedPtr talonOut as the parameter. 

### **void talon3Callback**(const messages::msg::TalonOut::SharedPtr talonOut):
Takes the SharedPtr talonOut and sends it to the send(std::string messageLabel, const messages::msg::TalonOut::SharedPtr talonOut) function with the label of "Talon 3".
#### Expected Input, Range(s) of Input
SharedPtr talonOut
#### Expected Outputs / Results, Range
Calls the send(std::string messageLabel, const messages::msg::TalonOut::SharedPtr talonOut) function with the label and SharedPtr talonOut as the parameter. 

### **void talon4Callback**(const messages::msg::TalonOut::SharedPtr talonOut):
Takes the SharedPtr talonOut and sends it to the send(std::string messageLabel, const messages::msg::TalonOut::SharedPtr talonOut) function with the label of "Talon 4".
#### Expected Input, Range(s) of Input
SharedPtr talonOut
#### Expected Outputs / Results, Range
Calls the send(std::string messageLabel, const messages::msg::TalonOut::SharedPtr talonOut) function with the label and SharedPtr talonOut as the parameter. 

### **void zedImageCallback**(const sensor_msgs::msg::Image::SharedPtr inputImage):
The function logs a message using RCLCPP_INFO from the rclcpp library, indicating that an image has been received. The logger used is retrieved from the nodeHandle object, which is assumed to be an instance of the rclcpp::node class
#### Expected Input, Range(s) of Input
SharedPtr inputImage
#### Expected Outputs / Results, Range
Logs if it received the image. 

### **std::string getAddressString**(int family, std::string interfaceName):
This is a C++ function named getAddressString that takes two arguments: family, an integer indicating the address family, and interfaceName, a string indicating the name of the network interface.

The function uses the getifaddrs function to retrieve a linked list of addresses of all network interfaces available on the system, and then iterates through this list using the ifa_next member.

For each network interface, it checks if its name matches the interfaceName argument, and if its address family matches the family argument. If both conditions are true, the function converts the address to a string representation and returns it.

There are three possible address families handled by the function:

AF_INET (IPv4) - the function uses inet_ntoa to convert the address to a string representation of the form "x.x.x.x".
AF_INET6 (IPv6) - the function converts each 16-bit block of the address to a hexadecimal string and separates them with colons.
AF_PACKET (MAC address) - the function converts each 8-bit block of the address to a hexadecimal string and separates them with colons.
Finally, the function frees the memory occupied by the linked list using the freeifaddrs function and returns the address string. 
#### Expected Input, Range(s) of Input
int family, string interfaceName
#### Expected Outputs / Results, Range
returns address as a string if found. 

### **void printAddresses**():
Debug function that logs the result of the function getAddressString(int family, std::string interfaceName) while it goes through all of the addresses.
#### Expected Input, Range(s) of Input
None
#### Expected Outputs / Results, Range
Prints what the getAddressString(int family, std::string interfaceName) function comes up with and prints when it's done.

### **void reboot**():
This function syncs and then calls the reboot() function with the parameter of LINUX_REBOOT_CMD_POWER_OFF.
#### Expected Input, Range(s) of Input
None
#### Expected Outputs / Results, Range
Reboots.

### **void broadcastIP**():
Checks if the broadcast variable is set to true. If broadcast is false, the function simply continues to the next iteration of the loop.

Calls the getAddressString function and passes AF_INET and "wlan0" as arguments to obtain the IP address of the interface wlan0.

Creates a message by concatenating the string robotName and "@" with the IP address obtained in step 2.

Creates a UDP socket using the socket function. If the socket is created successfully, the function continues. If the socket creation fails, the function continues to the next iteration of the loop.

Sets the address and port for the socket, the address is set to 226.1.1.1, which is a multicast IP address. The port is set to 4321.

Sets the local interface for multicast transmission by calling the setsockopt function and passing the socket descriptor, the IP protocol (IPPROTO_IP), the option name (IP_MULTICAST_IF), the local interface address and its size. If the call to setsockopt succeeds, the function continues. If it fails, the function continues to the next iteration of the loop.

Sends the message created in step 3 to the specified address and port by calling the sendto function.

Closes the socket by calling close.

Sleeps for 5 seconds. The function then repeats from step 1.
#### Expected Input, Range(s) of Input
None.
#### Expected Outputs / Results, Range
Establishes connection with socket. 

# Change Log:
7/3/2022: Documentation was created

2/4/2023: Documentation completed