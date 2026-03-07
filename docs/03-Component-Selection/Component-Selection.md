---
title: Module's Selected Major Components
---

## Module's Selected Major Components
Have not decided yet

The following sections are the selected major components necessary for  .....

>**For each of the following sections, use <ins>one of the two styles</ins> given near the end. *REMOVE THIS NOTE***

### Power Management

(**remove this note/placeholder**: this is where your 3.3 volt switching regulator, any other needed power regulator, and power source {if applicable} **THAT WERE SELECTED**)

For more details, review the ["Appendix - Component Selection Process - Power Mangement"](https://embedded-systems-design.github.io/EGR314DataSheetTemplate/Appendix/01-Componet-Selection/Component-Selection-Process/#power-management) selection.

### Sensor

(**remove this note/placeholder**: if applicable, this is where your  **SELECTED** sensor is shown. Otherwise, remove this section.)

For more details, review the ["Appendix - Component Selection Process - Sensor"](https://embedded-systems-design.github.io/EGR314DataSheetTemplate/Appendix/01-Componet-Selection/Component-Selection-Process/#sensor) selection.

### Actuator

(**remove this note/placeholder**: if applicable, this is where your **Selected** the actuator items go, which includes both the driver and motor. Otherwise, remove this section.)


### Table 1: Motor Driver

| Component | Pros | Cons |
|---------|------|------|
|  ![motor driver 1 image](https://github.com/user-attachments/assets/800e2dc6-bd3f-4044-a155-cdac0d122942) <br> -Choice 1 <br> -IFX9201SGAUMA1 <br> - Infineon Technologies <br> $3.55/each <br> -[Link](https://www.digikey.com/en/products/detail/infineon-technologies/IFX9201SGAUMA1/5415542) <br> -[Datasheet](https://www.onsemi.com/pdf/datasheet/lm2575-d.pdf) | -Used in class before <br> -Has CAD model <br> -Has High Voltage and Current Intake | -No reverse polarity protection <br> -Current has wide tolerance |
|  <img width="200" height="200" alt="image" src="https://github.com/user-attachments/assets/63ffbf3b-72db-4a41-874d-3367f02622ed" />    <br>  -Choice 2 <br>  -IC BRUSHED MOTOR DRVR 8TSSOP <br>   	-Toshiba Semiconductor and Storage <br> -$0.83/each <br> -[Link](https://www.digikey.com/en/products/detail/toshiba-semiconductor-and-storage/TB67H450AFNG-EL/15995284) <br> -[Datasheet](https://toshiba.semicon-storage.com/info/TB67H450AFNG_datasheet_en_20250730.pdf?did=70454&prodName=TB67H450AFNG) | -Inexpensive <br> -High Voltage & Current intake <br> -Has CAD file | -Only for DC brushed motors <br> -Sensitive thermal conditions  | 
|  <img width="200" height="200" alt="image" src="https://github.com/user-attachments/assets/606ccb0f-e37b-4324-836b-c4fcbfb50ea0" />  <br> -Choice 3 <br> -12-V, 1.76-A BRUSHED DC MOTOR DR <br> 	-Texas Instruments <br> -[Link](https://www.digikey.com/en/products/detail/texas-instruments/DRV8210DRLR/15286847) <br> -[Datasheet](https://www.ti.com/lit/ds/symlink/drv8210.pdf?HQS=dis-dk-null-digikeymode-dsf-pf-null-wwe&ts=1770877680405) | -Cheapest  <br> -Protection features <br> -Has CAD file | -Only for DC brushed motors <br> -Under 12V |

**Rationale:** Choice 1. We have used this motor driver in class and know how it works. It works with 12V and 3.3V logic. Choice 2 is a close second but it does not have SPI.


### Table 2: DC Motor

| Component | Pros | Cons |
|---------|------|------|
|  <img width="200" height="200" alt="image" src="https://github.com/user-attachments/assets/427120ef-6669-4ab0-9350-a32cda85099a" />  <br> -Choice 1 <br> -STANDARD MOTOR 6600 RPM 12V <br> 	-SparkFun Electronics <br> -$2.75/each <br> -[Link](https://www.digikey.com/en/products/detail/sparkfun-electronics/11696/6163657) <br> -[Datasheet](https://mm.digikey.com/Volume0/opasdata/d220001/medias/docus/951/ROB-11696_Web.pdf) | -Cheap <br> -Can intake 12V  <br> -2-wire setup | -Low torque <br> -Needs a custom footprint <br> -Little data on the datasheet |
| <img width="200" height="200" alt="image" src="https://github.com/user-attachments/assets/5d55a898-66d3-45e2-bcfa-d092ef51ee8b" /> <br> -Choice 2 <br> -GEARMOTOR 35 RPM 12V MICRO METAL <br> 	-Pololu <br> $37.95 <br> -[Link](https://www.digikey.com/en/products/detail/pololu/3046/10450048) <br> -[Datasheet](https://www.pololu.com/file/0J1487/pololu-micro-metal-gearmotors-rev-6-1.pdf) | -Uses 12V <br> -High torque <br> -2-wire connection | -High power <br> -Needs a custom footprint <br> -May be too slow |
| <img width="200" height="200" alt="image" src="https://github.com/user-attachments/assets/b3d44045-bbae-4623-bf88-854a9ccc35e4" />  <br> -Choice 3 <br> -GEARMOTOR 220 RPM 12V MICR METAL <br> -Pololu <br> -$26.45 <br> -[Link](https://www.digikey.com/en/products/detail/pololu/3042/10450044) <br> -[Datasheet](https://www.pololu.com/file/0J1487/pololu-micro-metal-gearmotors-rev-6-1.pdf) | -Steady speed <br> -2-wire connection <br> -Uses 12V | -Might be not enough torque/not fast enough <br> -May not be suitable for a drive train <br> -Needs a custom footprint |

**Rationale:** Choice 3. This motor has a good amount of speed and torque, and uses 12V, that it should be able to run our drive train well. 


### Table 3: 3.3V 1.5A Switching Power Supply
 To be determined <br>

| Component | Pros | Cons |
|---------|------|------|
| - | - | - |


### Table 4: 12V 2A AC-DC Wall Power Supply

| Component | Pros | Cons |
|---------|------|------|
| ![12V Wall Power 1](https://github.com/user-attachments/assets/851bcc5a-d03c-4438-b80b-d4cf19db04fa)     <br>  -Choice 1  <br> L6R24-120  <br> -Tri-Mag, LLC   <br> -$10.38/each   <br> -[Link](https://www.digikey.com/en/products/detail/tri-mag-llc/L6R24-120/7682639) <br> -[Datasheet](https://www.tri-mag.com/wp-content/uploads/2021/05/L6R24-L6R30_Series_2021-02.pdf) | -Inexpensive  <br> -Has less noise  <br> Average Efficiency | -The cord is short | 
|  ![12V Wall Power 2](https://github.com/user-attachments/assets/969ed2ea-2765-4eba-a302-e7469fd92a16)    <br>  -Choice 2  <br> -WSU120-2000  <br> -Triad Magnetics  <br> -$15.07 each  <br> -[Link](https://www.digikey.com/en/products/detail/triad-magnetics/WSU120-2000/3094983) <br> -[Datasheet](https://catalog.triadmagnetics.com/Asset/WSU120-2000.pdf) | -Average Efficiency  <br> -Inexpensive | -More Expensive  <br> -Has more noise |
| ![12V Wall Power 3](https://github.com/user-attachments/assets/49f281c1-7b19-4a5e-b7aa-e597b33bff10)      <br>  -Choice 3  <br> MDS-030AAC12 AB  <br> -Delta Electronics  <br> -$29.26/each  <br> -[Link](https://www.digikey.com/en/products/detail/delta-electronics/MDS-030AAC12-AB/6150232)  <br> -[Datasheet](https://psu.deltaww.com/en/products/download/Datasheet/MDS-030AAC05) | -Medical Power Supply  <br> -Average Efficiency | -Very Expensive  <br> -Big |

**Rationale:** Choice 1. This power supply has low output noise and is not too expensive. The other power supplies are around the same, but choice 2 has more noise, and choice 3 is overkill, as it is for medical devices.







