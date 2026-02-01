---
title: Module's Requirements
---

## Module Requirements
This table shows the requirements for my module of our system. It is one of the motor modules that will move a wheel on our robot. The table lists out the requirements for the module to work, as well as how the requirement is measured, and what is the lowest measure to not fail.

| **Requirement<br>Description** | **Measure of<br> Threshold** | **Target<br>Measure** |**Stretch<br>Requirement<br>(Y-N)**|
|-----------------------------| ----------------- | ----------------- | :-----: |
| Surface mounted, 3.3V switching power regulatore | 3.2 Volts | 3.3 Volts | No |
| Surface mounted microcontroller | 1 PIC or ESP | ESP32 | No |
| Wireless Communication | Able to send or receive a Wi-Fi data | Send and receive Wi-Fi Data to MQTT | Yes |
| DC Motor | Able to move our robot | Has enough torque to move the robot | No |
| Motor Driver | Able to control the speed of the motor | Control the speed of the motor and move it forwards and backwards | No |
| Hall Effect Sensor | Able to track information about the motor | Send information about the motor (IE: Speed, Posiotion, Displacement) to the microcontroller | No |
| LED | Tell the user what is going on | Lights up when an error occurs, or when everything is running good | Yes |
| Battery | Output power and last a while | Output 9 or 12V (depending on the motor requirements), and last for at least 10 minutes | No |
