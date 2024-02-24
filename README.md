# PARATEC
Paralyzed Assistive Robotic Arm eye Tracking and Electric Chair

# Introduction
![image](https://github.com/adnanO999/PARATEC/assets/88556508/365d5e26-3160-4d6c-8acf-1079afe8fd88)

Autonomy is a fundamental aspect of human life, influencing our ability to interact with the world and lead enjoyable lives. For individuals living with paralysis, however, autonomy is often a wish, presenting significant challenges in everyday tasks and activities. In response to this critical issue, we introduce “PARATEC—The Paralyzed Assistive Robotic Arm, eye-Tracking and Electric Chair” to make wishes come true and empower paralyzed individuals by restoring their autonomy through an integrated system. This system is fully developed from scratch and comprised of a robotic arm built using additive manufacturing (3D printing), used to achieve activities of daylily living (ADL) such as feeding process of the patient, an electric wheelchair designed from the ground up to facilitate transportation and an eye tracking system offering an innovative solution and a user-friendly interface for individuals with limited physical mobility. These parts are connected all together through a website application. In this report we aim to present PARATEC not just as a technological innovation but as a comprehensive solution for autonomy problem tackling a detailed overview of the hardware and software employed.

# Robotic Arm
![image](https://github.com/adnanO999/PARATEC/assets/88556508/6964932d-5917-4c0f-b0ed-e71610f767ad)

The main focus of the section is to describe the heart of our project that is the robotic arm feeder. Our aim is to develop a methodology for creating a printable low budget, reliable, effective solution assistive device and six degrees of freedom robotic arm. After extensive research and exploration of the available models we selected the best solution that is based on open-source robotic arm which resemble the UR3 robotic arm. 3D printable 6DOF robotic arm that is similar to universal robot with an 80% scale. The printable arm is scaled-down version inspired by the UR3 robotic arm. The design preserves the essential features of the original while reducing its size by 20%, making it suitable for applications where space and weight considerations are crucial as in our application. The model can be divided into two main parts: the first 3DOF forming the body of the arm and the last 3DOF forming the wrist. All components of the robotic arm are designed for 3D printing, enhancing accessibility and allowing for cost effective manufacturing. Thus, accurate and durable parts can be created, ensuring the structural integrity of the arm. The chosen model will be modified, enhanced and customized to fit our needs. 

## Solidworks Design
Robotic manipulators are usually built of an assembly of joints and links. Joints can be represented as connection between two links, and by links we mean the rigid connection between two joints. Finally, the end effector or tool tip is the device which interact with the environment. After several research iterations, the model that we found was downloadable as step file which means we cannot modify the parts. In order to do so, we need to recreate the parts using a CAD software. For this reason, SolidWorks used to redraw the model according to the measured dimensions from the step file. The model can be divided into several parts:
•	Base link and actuator
•	Shoulder link and actuator
•	Elbow link and actuator
•	Wrist actuators (x3)

