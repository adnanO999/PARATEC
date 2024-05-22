# PARATEC
Paralyzed Assistive Robotic Arm eye Tracking and Electric Chair
![image](https://github.com/adnanO999/PARATEC/assets/88556508/8c00c7e4-aafe-4fb6-ae3f-0927e9f0461e)

# Introduction
![image](https://github.com/adnanO999/PARATEC/assets/88556508/365d5e26-3160-4d6c-8acf-1079afe8fd88)

Autonomy is a fundamental aspect of human life, influencing our ability to interact with the world and lead enjoyable lives. For individuals living with paralysis, however, autonomy is often a wish, presenting significant challenges in everyday tasks and activities. In response to this critical issue, we introduce “PARATEC—The Paralyzed Assistive Robotic Arm, eye-Tracking and Electric Chair” to make wishes come true and empower paralyzed individuals by restoring their autonomy through an integrated system. This system is fully developed from scratch and comprised of a robotic arm built using additive manufacturing (3D printing), used to achieve activities of daylily living (ADL) such as feeding process of the patient, an electric wheelchair designed from the ground up to facilitate transportation and an eye tracking system offering an innovative solution and a user-friendly interface for individuals with limited physical mobility. These parts are connected all together through a website application. In this report we aim to present PARATEC not just as a technological innovation but as a comprehensive solution for autonomy problem tackling a detailed overview of the hardware and software employed.

# Robotic Arm
![image](https://github.com/adnanO999/PARATEC/assets/88556508/6964932d-5917-4c0f-b0ed-e71610f767ad)

The main focus of the section is to describe the heart of our project that is the robotic arm feeder. Our aim is to develop a methodology for creating a printable low budget, reliable, effective solution assistive device and six degrees of freedom robotic arm. After extensive research and exploration of the available models we selected the best solution that is based on open-source robotic arm which resemble the UR3 robotic arm. 3D printable 6DOF robotic arm that is similar to universal robot with an 80% scale. The printable arm is scaled-down version inspired by the UR3 robotic arm. The design preserves the essential features of the original while reducing its size by 20%, making it suitable for applications where space and weight considerations are crucial as in our application. The model can be divided into two main parts: the first 3DOF forming the body of the arm and the last 3DOF forming the wrist. All components of the robotic arm are designed for 3D printing, enhancing accessibility and allowing for cost effective manufacturing. Thus, accurate and durable parts can be created, ensuring the structural integrity of the arm. The chosen model will be modified, enhanced and customized to fit our needs. 

## Solidworks Design
Robotic manipulators are usually built of an assembly of joints and links. Joints can be represented as connection between two links, and by links we mean the rigid connection between two joints. Finally, the end effector or tool tip is the device which interact with the environment. After several research iterations, the model that we found was downloadable as step file which means we cannot modify the parts. In order to do so, we need to recreate the parts using a CAD software. For this reason, SolidWorks used to redraw the model according to the measured dimensions from the step file. The model can be divided into several parts:
*	Base link and actuator
*	Shoulder link and actuator
*	Elbow link and actuator
*	Wrist actuators (x3)
![image](https://github.com/adnanO999/PARATEC/assets/88556508/47ad0323-f766-4d1c-b040-6c226ea90b90)
![image](https://github.com/adnanO999/PARATEC/assets/88556508/e1296c40-2471-4fa7-a2af-59f6560a8073)
![image](https://github.com/adnanO999/PARATEC/assets/88556508/bf9825b5-dc8c-4777-8c3a-9ce50497433d)

## Hardware Architecture
![image](https://github.com/adnanO999/PARATEC/assets/88556508/78d190d8-aede-4c54-8919-bc35da6bbd0d)

The robotic arm is an essential part of the project. It is responsible of feeding the patient along with accomplishing additional tasks in future work. The components of the arm should be available in the market for several reasons: spare parts and affordability. We tried our best to have all components from local stores except for encoders. The reason will be explained in details along with choice alternatives. In what follows we will explain the functionality of each component along with the mode of operation in our design.
### Microcontroller
The Arduino Mega will be the main controller.  It has 54 digital input/output pins (of which 15 can be used as PWM outputs), 16 analog inputs, 4 UARTs (hardware serial ports), a 16 MHz crystal oscillator, a USB connection, a power jack, an ICSP header, and a reset button. It contains everything needed to support the microcontroller. Regarding memory usage, it has 8 KB of SRAM and 256 KB of Flash memory making it suitable for our application. In addition, we have four interrupt pins that makes it suitable for using multiple interrupt subroutine (ISR) to capture any signal for example limit switches signal without interruption of the main program. The only drawback is that only one I2C channel is available.

### Raspberry Pi
The Raspberry Pi is a low-cost computer that runs Linux-based Raspbian, and it also provides a set of GPIO (general purpose input/output) pins which is the reason why sensors can interface with it. Additionally, it has the required processing power to control a lower-level microcontroller (such as the Arduino UNO), and process images and video content since it has a CPU, a GPU, internal memory, and ports that make it easy to connect to it. In our project the raspberry pi will be used for processing images generated from RGB-D camera.

### RGB-D Camera
An RGBD camera is a type of depth camera that provides both depth (D) and color (RGB) data as the output in real-time. Depth information is retrievable through a depth map/image which is created by a 3D depth sensor such as a stereo sensor or time of flight sensor. A time-of-flight camera (ToF camera), also known as time-of-flight sensor (ToF sensor), is a range imaging camera system for measuring distances between the camera and the subject for each point of the image based on time-of-flight, the round-trip time of an artificial light signal, as provided by a laser or an LED. In our case we wanted an affordable solution to measure how deep the end effector should move either to grab the object or to feed the patient. We selected the arducam TOF RGB-D camera due to its low cost and ease of integration in our project.
![image](https://github.com/adnanO999/PARATEC/assets/88556508/36d13c79-fd55-4adc-bec5-0a9f51812d5f)
 


### Limit Switches
Limit switches are used to create home configuration for our robotic arm. When one link touches the limit switches that is installed in a predefined position, a signal will be sent to interrupt the action of the stepper motors and stop them. This is essential to have a reference or initial position of the arm. The reference is selected to derive the equation of motion for the arm. Limit switches are considered as electrical stoppers. Future work should include mechanical stoppers for additional safety purposes. The figure below shows the connection of a micro limit switch with a pull-down resistor.

![image](https://github.com/adnanO999/PARATEC/assets/88556508/b41f11ed-e412-4946-bd1d-ed9b99c3b717)

  
### Stepper Motor
Stepper motors were selected due to the advantageous performance they offer compared to servo motors or geared DC motors. The advantages rely in the performance, accuracy and price. Listed below are the advantages of using stepper motor:
•	Precise control: Stepper motors move in discrete steps, providing accurate position control.
•	No feedback required: Stepper motors can be operated with no feedback devices like encoders for position verification.
•	Relatively simple control: Stepper motors are often easier to control in open-loop systems.
 
![image](https://github.com/adnanO999/PARATEC/assets/88556508/1d73de50-e47b-449c-ade5-71cf0044f302)

The used stepper motor is formed of two coils. Each coil has two wires forming a two phases motor. Input pulses (composed of square waves) are transformed into accurate increment in rotational position. Each pulse rotates the shaft through a fixed angle. The normal step is 1.8 degree and can be decreased by use of micro stepping technics, the smallest step is reached when the stepper is operating in quadrature mode which means the original step is divided by four making a step of 0.45 degree. When operating in full step, one full revolution will consist of 360/1.8 steps which is equivalent to 200 steps per revolution. A stepper motor moves one step when the direction of current flow in the field coil(s) changes, reversing the magnetic field of the stator poles. The bipolar motor has one coil per phase and needs two changeover switches, or a full-bridge, for each phase. In our case the full-bridge will be implemented using the a4988 stepper motor drive. Below are some characteristics of our selected Nema 17 stepper motor:
*	Rated Voltage: 12 V DC
*	Current/phase: 1.4~1.7 A
*	Number of Phases: 2
*	Step Angle: 1.8 degree
*	Holding Torque: 0.59 N.m
  
### Encoder
While stepper motors do not require feedback loop to operate as stated earlier, we imposed the use of encoders to close the loop and obtain precise control over the steppers. This is crucial since the position of the end effector might deviate from the desired position due to outside factors such as friction. This creates the need of selecting encoder types for our application. Several alternatives are available for feedback and position control. Optical encoders, hall effect encoders, magnetic encoders along with a completely different type od sensors which is the inertial measurement unit (IMU) are available. In our research we investigated the use of different type of sensors and we tried the use of magnetic encoders and IMU. The advantages and disadvantages of each sensor will be discussed along with the experimental results obtained.
For our project we selected the AS5600 encoder. The AS5600 is an easy to program magnetic rotary position sensor with a high-resolution 12-bit analog or PWM output. This contactless system measures the absolute angle of a diametric magnetized on-axis magnet. This AS5600 is designed for contactless potentiometer applications and its robust design eliminates the influence of any homogenous external stray magnetic fields. By default, the output represents a range from 0 to 360 degrees. It is also possible to define a smaller range to the output by programming a zero angle (start position) and a maximum angle (stop position). The AS5600 is also equipped with a smart low power mode feature to automatically reduce the power consumption. This sensor is suitable for angular position measurement. The block diagram of the sensor is showing the pinout is shown below:
 
![image](https://github.com/adnanO999/PARATEC/assets/88556508/bde70072-2cc2-4c54-899e-f3fee90d7660)

The below table summarizes the pin description and specifies which pins are essential to use in our application:
![image](https://github.com/adnanO999/PARATEC/assets/88556508/a3db7cb0-5f90-4a9e-94f8-f6ff99a2e704)

In summary the as5600 is a hall-based rotary magnetic position sensor using planar sensors that convert the magnetic field component perpendicular to the surface of the chip into a voltage. This signal is first amplified and filtered before being converted by the ADC. The output of the ADC is processed to compute the angle and magnitude of the magnetic field vector. The angle value provided by the coordinate rotational digital computer (CORDIC) is used by the output stage.
This encoder transmits and receives data through the I2C interface. The AS5600 always operates as a slave on the I²C bus. Connections to the bus are made through the open-drain I/O lines SDA and the input SCL. Clock stretching is not included. The host MCU (master) initiates data transfers. The 7-bit slave address of the AS5600 is 0x36 (0110110 in binary). This address cannot be changed and having only one I2C channel on the Arduino, we are required to use a multiplexer to connect simultaneously six encoders on the same channel.

### Multiplexer
The TCA9548A I2C multiplexer allows the communication with up to 8 I2C devices with the same I2C bus. The multiplexer communicates with a microcontroller using the I2C communication protocol. Then, allows to select which I2C bus on the multiplexer we want to address. The TCA9548A is an 8-channel, bidirectional translating I 2C switch. The master SCL/SDA signal pair is directed to eight channels of slave devices, SC0/SD0-SC7/SD7.
 ![image](https://github.com/adnanO999/PARATEC/assets/88556508/9f0fbe50-4cba-4857-a515-befbb756e3ad)

### Stepper Drive
In order to send signal to our stepper motors a drive is required. Taking into consideration the power required by the stepper motor, we selected a suitable drive having low cost and high reliability. The selected drive is a4988 which offers the ability of current limiting, this means that if the stepper needs to draw more current, higher than the rated value, the stepper has the ability to limit the current to a certain threshold. The circuit diagram of the drive along with its functionality are provided below:

Figure 59 A4988 Pin Out
The A4988 is a complete micro stepping motor driver with built-in translator for easy operation. It is designed to operate bipolar stepper motors in full-, half-, quarter-, eighth-, and sixteenth-step modes, with an output drive capacity of up to 35 V and ±2 A. The A4988 includes a fixed off-time current regulator which has the ability to operate in Slow or Mixed decay modes. As mentioned in the stepper section, each phase is driven by a full H-bridge. If we go on the electronic level we can see the implementation of the full H-bridge using transistor specifically MOS type:
![image](https://github.com/adnanO999/PARATEC/assets/88556508/75f2fafb-5e61-4d51-b9ce-3c1b3b7989c3)
Full H-bridge Implementation and Stepper Connection

### Overall Circuit Diagram

The below picture shows a printed circuit board (PCB) fully implemented using EasyEDA. The PCB contains six A4988 stepper drivers along with decoupling capacitors connected between ground and VCC of each module. This is called a bypass capacitor used to prevent noise from entering the system by bypassing it to the ground. It reduces power supply noise and voltage spikes on the supply lines.
![image](https://github.com/adnanO999/PARATEC/assets/88556508/fd3b0e74-2d46-449b-8b39-b31e2614e844)
Wiring Diagram of the Stepper Drivers Connection

This schematic was converted in PCB design by routing all wires in a convenient method. The PCB is formed of several layers including upper and lower copper layers which makes routing easier. Below is the routed circuit
 ![image](https://github.com/adnanO999/PARATEC/assets/88556508/df5cfd8e-b1f4-41a2-a48d-bca1449d2803)
 ![image](https://github.com/adnanO999/PARATEC/assets/88556508/99854a5a-cca3-482e-ad22-87539ee29d66)
 ![image](https://github.com/adnanO999/PARATEC/assets/88556508/e0ab16c1-5ade-47c7-bc2c-81ca45d1d959)

 This was the first part of the electric part. The second part contains a PCB layer dedicated for multiplexer, encoders and limit switches along with additional pins for future sensors to be included such as force/torque sensor.
![image](https://github.com/adnanO999/PARATEC/assets/88556508/e619ae86-1c44-4710-8e73-d6e9d346cd18)
![image](https://github.com/adnanO999/PARATEC/assets/88556508/ddf119b7-6eb8-4b68-b87f-1d0c77955157)
![image](https://github.com/adnanO999/PARATEC/assets/88556508/cea96d8f-014b-4709-9c44-efd2383d4882)


## Motion Generation
### Gears
Gears are mechanical transmission elements used to transfer motion and power between the input and output of device or two different parts such as motor and shaft. An intermediate connection between the two is required to enhance performance and increase either speed or torque, one at the expense of the other. In most of the applications we are interested in increasing the torque, since we are limited by the motor size and rated output torque. Each joint is composed of “split ring compound planet epicyclic gear system”. This type of motion transmission eliminates the use of extra components such as belts, pulleys and tensioner and can be fully 3D printed. High quality prints will give longer gear life along with higher accuracy as was mentioned in previous sections related to 3D printing methods. In addition, using gears gives higher gear ratios which induces more torque. To elaborate more, this arm is designed to have minimal mechanical components with higher reliability and efficiency. The designed components are only gears with high enough gear ratio to compensate for the arm weight and handle enough torque. The design is special and give dual functionality. The inner gear is a split compound planetary gear with a gear ratio of 38.4:1. Each link is attached to the ring of the planetary gear, thus to maintain equilibrium and ensure proper rotation, the rings is held in an aligned position by mean of metal spheres. By this technique, we are creating a thrust bearing capable of handling axial and radial loadings. We should mention also that gears have helical profile which gives them higher immunity for noise reduction

![image](https://github.com/adnanO999/PARATEC/assets/88556508/61675259-9ae9-4b01-8624-6816aca02544)
![image](https://github.com/adnanO999/PARATEC/assets/88556508/2402e2d2-48ac-49a1-a587-e33d3b740e3f)

### Thrust Ball Bearing
A thrust bearing is a type of bearing designed to support axial loads, which are forces that act parallel to the axis of rotation. Unlike radial bearings, which support loads perpendicular to the shaft, thrust bearings are specifically engineered to handle forces pushing or pulling along the shaft. This is exactly what we need since we have parallel forces pushing on the shaft. Below are pictures of the mechanism designed
![image](https://github.com/adnanO999/PARATEC/assets/88556508/b783dbf8-d2e6-4f80-8d59-3482c75b6c2a)

# Control System
![image](https://github.com/adnanO999/PARATEC/assets/88556508/788e7bed-2266-4c6d-aa7e-73ed55ed36c1)

The process of controlling the robotic arm will be based on kinematics and dynamics equations. The desired position will be fed as input. The inverse kinematics will translate this position into joint angle than these angles will be passed to the forward kinematics block to recompute the real position which will be compared to the desired position. This will give us the tracking error that will be adjusted using PID controller. The feedback is obtained through encoders. This is in brief the control system architecture. The detailed implementation steps are listed below:
## Forward Kinematics:
*	Assigning frames to each joint using Denavit-Hartenberg convention
*	Deriving transformation matrix for each frame relative to its predecessors 
*	Calculating the forward kinematics by using matrices multiolication
## Inverse Kinematics:
*	Decoupling the position and orientation task
*	Solving graphically using mathematical and geometrical relations to solve for angle joints
Future work will implement in details the equations obtained along with overall control block. A physic engine might be employed to facilitate the control part of the arm. Such system can use Robotic Operating System (ROS) due to the wide tools offered to build robotic manipulators.
These steps were implemented using MATLAB than written in C++ using Arduino IDE. The below figures show the code implementation.

![image](https://github.com/adnanO999/PARATEC/assets/88556508/bbabaa5a-b447-41fb-a3af-81e330233ed8)

# ROS Integration
![image](https://github.com/adnanO999/PARATEC/assets/88556508/480f48bd-9ab9-4dad-9c65-506b79dd6dee)

* Building the URDF
* Digital twin: Rviz and Gazebo
* Implementing controler manager
* Implementing hardware interface
* MoveIt configuration
  
## In Depth Control

# Electric Wheel Chair









