# File: PowerDistributionPanel.cpp
## Author: Bill Johnson
## Documentation Author: Andrew Burroughs
## Detailed Description: 
The PowerDistributionPanel.cpp file contains the implementation of a class that represents a power distribution panel. The class includes functions to read current and voltage measurements, as well as control the state of individual power outlets. The purpose of this class is to provide a simple interface for monitoring and controlling the power distribution panel.

This file is using the `ncurses` library and the `can_frame` struct from the Linux SocketCAN framework. The code has hardcoded the power panel to an id of 1 which may need to be changed in future implementations.

## Issues:
None

# Software Documentation
## Global Variables
### **float voltage**
The current voltage.

### **float currentA[15]**
The current values for a specified source.

### **float currentB[15]**
The current values for a specified source.

### **float currentC[15]**
The current values for a specified source.

## Function Documentation
### **PowerDistributionPanel**():
A constructor for the class, initializing the voltage property to 0.


### **float getCurrent**(int source):
This method returns the value of the currentC of the specified source. Note that this function is seemingly redundant as it returns the same as `getCurrentC(int source)` but is not called in the respective node file.


### **float getCurrentA**(int source):
This method returns the value of the currentA of the specified source.


### **float getCurrentB**(int source):
This method returns the value of the currentB of the specified source.


### **float getCurrentC**(int source):
This method returns the value of the currentC of the specified source.

### **float getVoltage**():
This method returns the current voltage.


### **void parseFrame**(struct can_frame):
This method parses a given can_frame and updates the class properties based on the can_id in the frame.

#### Expected Input:
frame – struct can_frame  
#### Expected Results:
This function will call either the `parseVoltage` and/or `parseCurrent` of the inputted frame depending on the `can_id`. 


### **void parseVoltage**(struct can_frame frame):
This method parses the voltage from a given can_frame and updates the voltage property.

#### Expected Input:
frame – struct can_frame  
#### Expected Results:
This function will check the `can_id` of the inputted frame and if the input is valid, the volatge variable will be updated to `.05*frame.data[6]+4`.


### **void parseCurrent**(struct can_frame frame):
This method parses the current values from a given can_frame and updates the currentA, currentB, and currentC properties. The function starts by declaring a constant currentScalar with a value of 0.125. Then, it performs several bitwise operations and arithmetic operations to extract current information from the data member of the struct can_frame object and store it in different arrays of the class, such as currentA, currentB, and currentC. The specific array that the information is stored in depends on the value of the can_id member of the struct can_frame object.

#### Expected Input:
frame – struct can_frame  
#### Expected Results:
This function will check the `can_id` of the inputted frame and depending on the `can_id` of the frame, it will update the corresponding current array (A, B, or C) with current values that are determined based on calculations from the frame's binary data representing the current value of the electrical circuit.


# Change Log:
7/3/2022: Documentation was created

2/4/2023: Documentation completed




