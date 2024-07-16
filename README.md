# Jabber Robot Arm

## Overview

Jabber is a five-servo robot arm designed as a final project for the ECE 350 course at Duke University. It can be manually controlled using joysticks and switches on a Nexys A7 FPGA board or programmed for automated movements. This README provides an in-depth overview of the project, including its hardware setup, software implementation, and challenges faced during development.

## Table of Contents
1. [Introduction](#introduction)
2. [Hardware](#hardware)
3. [Software](#software)
4. [Inputs and Outputs](#inputs-and-outputs)
5. [Custom Processor Modifications](#custom-processor-modifications)
6. [Challenges](#challenges)
7. [Testing](#testing)
8. [Assembly Programs](#assembly-programs)
9. [Improvements](#improvements)
10. [Conclusion](#conclusion)
11. [Media](#media)

## Introduction
Jabber is a five-servo robot arm controlled using two joysticks and switches on the Nexys A7 FPGA board. The arm has four axes of rotation and a claw grip for picking up small objects. Manual control is achieved through the joysticks, while a custom movement mode can be activated via a switch on the FPGA board, allowing for predefined movements in an assembly loop.

## Hardware
### Components
- **3D-Printed Body**: Designed using Fusion 360 and printed using Duke’s 3D-printing resources. Most parts were sourced from Thingiverse and modified as needed.
- **Servos**: 
  - One 20 kg load servo for the shoulder.
  - Three MG996R servos for the elbow and wrist.
  - One MG90S servo for the gripper.
- **Joysticks**: Two arcade joysticks with four outputs each (up, down, left, right), operating at 5V.
- **Level Shifters**: Used to convert PWM signals from 3.3V (FPGA) to 5V (servo input).
- **Power Supply**: Wall adapter providing 5V to servos and joysticks.

### Assembly
- **Servo Integration**: The servos were chosen based on torque requirements, with the 20 kg servo used for the shoulder due to its high torque capacity.
- **Gear Modifications**: Lego gears were used to improve the reliability of the gripper mechanism.
- **Voltage Dividers**: Simple voltage dividers were constructed to interface the 5V joystick signals with the 3.3V FPGA inputs.

## Software
### PWM Signal Generation
- **PWM Serializer**: Custom modules were created to generate the necessary PWM signals for the servos, reading duty cycles from registers.
- **Manual Control**: Joystick inputs were decoded to update duty cycles in registers corresponding to each servo.

### Custom Movements
- **Assembly Code**: Custom movements were defined in assembly, specifying duty cycles for each servo and incorporating delay instructions to control timing.
- **Manual vs. Automated Modes**: A switch on the FPGA toggles between manual control and predefined automated movements.

## Inputs and Outputs
- **Joystick Inputs**: Each joystick provides four active-low signals, which are read into specific registers on the FPGA.
- **Servo Outputs**: PWM signals are generated based on register values, controlling the position of each servo.
- **Switches**: Used to toggle the gripper and switch between manual and automated control modes.

## Custom Processor Modifications
### Delay Instruction
- **Implementation**: A custom delay instruction was added to the processor, allowing for precise control over timing in automated movements.
- **Registers**: Two new 64-bit registers (`current` and `count_till`) were introduced to manage clock cycle counts for delays.

## Challenges
### Button Bounce
- **Issue**: Button bounce on the FPGA caused erratic behavior in manual control.
- **Solution**: Replaced button inputs with more stable switches, resolving the issue.

### Gear Mechanism
- **Issue**: Initial gear setup for the wrist servo was unreliable.
- **Solution**: Replaced with Lego gears, providing a more stable mechanism.

## Testing
- **Oscilloscope and Power Supply**: Used to test continuity and PWM signal functionality.
- **Version Control**: Employed during integration to isolate changes and debug issues.

## Assembly Programs
### Manual Movement
- **Joystick Control**: Decoded joystick inputs to update servo duty cycles, with boundary checks to prevent overextension.
- **Continuous Update**: Joystick values were latched every 20ms to ensure responsive control.

### Custom Movements
- **Predefined Sequences**: Automated sequences were defined using measured duty cycle values for specific positions, ensuring smooth transitions between movements.

## Improvements
### Servo Replacement
- **Mini Servo**: Plan to replace the mini servo in the gripper for increased reliability.
### Easier Custom Movements
- **Record Mode**: A proposed improvement involves a “record” mode to store PWM values in memory for easier creation of custom movements.

## Conclusion
Jabber successfully integrated hardware and software, providing both manual and automated control of a robot arm. Despite various challenges, the project was completed as a minimum viable product and laid the foundation for future enhancements. The project provided valuable learning experiences in robotics, hardware, and software integration.

## Media
### Videos
- [Manual Movement](#): *(Insert link to video of the robot performing manual movements)*
- [Automated Movement](#): *(Insert link to video of the robot performing automated movements)*

### Images
- ![Robot Arm Dimensions](path/to/dimensions-image.jpg): *(Insert an image showing the dimensions of the robot arm)*

## Authors
- **Humza Chouhdry**
- **Harrison York**

## Acknowledgments
- **Duke University**: For providing resources and support.
- **Thingiverse and Fusion 360**: For design and 3D printing resources.
- **ECE 350 Course**: For the foundational knowledge and project guidance.
