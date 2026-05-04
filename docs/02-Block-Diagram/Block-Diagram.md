---
title: Module's Block Diagram
tags:
- tag1
- tag2
---

## Overview
This block diagram is for my specific module for Team 301's project. My module is part of the drive train that will move our robot. The circuity will require specific voltage levels, such as 3.3V for the logic of the ESP32 and the logic for the motor driver, and 12V to power the motor. I will be using a 12V DC motor to drive half of the drive train of our robot. I will use a motor driver to control the motor and allow it to move forwards and backwards. We will be connecting to each other with UART and GPIO pins. It will be powered by a 12V 2A AC/DC power supply that will connect to a 3.3V switching power regulator.

<br>

I started with the template, but I did not need to have both the ESP32 and the PIC microcontrollers, so I removed the PIC and replaced it with the ESP32. I then put all of my components, my motor driver and motor connected to SPI and GPIO pins. My LED and button are connected to GPIO pins, and my voltage regulator connected to my power supply. Then I did my header pins, having shared power on pin 1, shared ground on pin 8, UART on pin 2, and I have some extra GPIO pins on 3 and 4 in case we wanted to send something not over UART. My block diagram meets my project requirements as a motor node, as I have a motor driver and motor, as well as an LED and button to debug when necessary, and the class standard of ribbon cable pinouts.


## Block Diagram 

<img width="831" height="742" alt="314 Individual Block Diagram BW drawio" src="https://github.com/user-attachments/assets/6019da30-6db3-41c2-ba37-41b7a78ed8d7" />

<br>

My source file link for draw.io can be found [here.](https://embedded-systems-design.bitbucket.io/314/individual-assignments/block-diagram/Block%20Diagram-314.drawio)

The image of the souce file is [here.](https://github.com/user-attachments/files/27330418/EGR.314.Template.drawio.zip)


