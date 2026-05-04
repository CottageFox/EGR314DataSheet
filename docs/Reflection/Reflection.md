---
title: Reflection
---

## Review of Module's Success

For my module's requirements, I succeded in almost all of them. I have a 3.3V switching regulator that is surface mounted. I have a surface mounted ESP32. I was able to send a recieve data with UART, I did not send anything to the server but that part was a stretch goal. I have a DC motor that was able to move our wheels on our prototype. I had a surface mount motor driver that used SPI. I also had an LED that would do a few things depending on what I was trying to look at. The requirements that were missed are the Hall Effect sensor and Battery. When designing my module, I realized that a hall effect sensor would be its own module entirely, so it would have been too confusing to try and do both on one module, so we made it a stretch goal and did not include it. Finally the battery, we never really talked about using one once we were designing our modules, so it just got lost in the idea phase and we never got one.


## Microcontroller/Module Startup Tip

-  Make sure that your SPI or I2C pins are correct, if they are wrong it will not work.
-  Make sure your USB pins are correct, if they are wrong or even flipped, you will not be able to connect to your computer.
-  For the ESP32 check the IO number on the pins, not the pin number themselves when doing the pinout.


## Lessons Learned

There are a lot of things that I have learned from this class as the project went on. Make sure to look at all of the datasheets of your parts multiple times. If an important pin is wrong, then the whole thing may not work. Double check your pin connections in the schematic, you do not want to have to redo the entire thing becaue of a wrong placement for a pin. For the PCB, make sure you use the correct footprints for your parts, surface mounted parts will not fit if the sizing is wrong. After my first design I realized that the numbers matter on the parts that you buy. If you have a part that is 0805, the smallest the class reccomends, then you need an 0805 footprint. Bigger may work, but smaller definetly wont fit. And if you have a weird size like 1210, thats wider than 1206, then it has to be bigger as well. Basically make sure that you understand what you are buying and how small it really is, becuase surface mounted parts can be like half a milimeter big, unlike a trough hole resistor thats like an inch long. Also for motor users who are using their raw power to power the motor, make sure that you have enough jumpers or seperation on your PCB, or else the shared power will be connected even if you do not connct it. I wired all of my 12V lines together including my shared power, and I had to cut a trace so I did not damage my teamate's boards.


## Recommendations for future students
1. Work ahead, you might regret it if you fall behind.
2. Ask for help, the professor and TA's will work with you, but only if you ask for it.
3. Pay attention in class, the information that is given is very useful, and may only be said once or twice.
4. Work on the physical prototype early, like when you order your parts, because you will not have a lot of time in the end of the class to do it.
5. Ask someone to check that your design is good and makes sense before you order your parts. It may be too late when you realize that you ordered something too small, or may be very hard to work with.
