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


### Table 1: Hall Effect Sensor

| Component | Pros | Cons |
|---------|------|------|
|  ![Hall Effect Sensor 1](https://github.com/user-attachments/assets/d7a010bf-4280-4f01-a04b-e3f10b7f98b4)  <br> -Choice 1  <br> -AS5600-ASOM  <br> -ams-OSRAM USA INC.  <br>  -$3.17/each  <br> -[Link](https://www.digikey.com/en/products/detail/ams-osram/AS5600-ASOM/4914332) <br> -[Datasheet](https://www.digikey.com/html/datasheets/productinfo/1647438/0/0/1/as5600-datasheet.pdf) | -Have worked with this before <br> -More output modes | -Hard to work with  <br> -Has more pins, harder to wire  <br> -Most Expensive |
|  ![Hall Effect Sensor 2](https://github.com/user-attachments/assets/28da5486-a231-4f36-b95a-c55579f82a12)   <br>  -Choice 2  <br> -TMAG5273 Low-Power Linear 3D Hall-Effect Sensor  <br> -Texas Instruments  <br> -$1.24/each  <br>  -[Link](https://www.mouser.com/ProductDetail/Texas-Instruments/TMAG5273D1QDBVR?q=IKkN%2F947nDf5iy%252BbYuEbTg%3D%3D) <br> -[Datasheet](https://www.ti.com/lit/ds/symlink/tmag5273.pdf?ts=1770822612850&ref_url=https%253A%252F%252Fapp.ultralibrarian.com%252F) | -Has fewer pins, so it’s easier to wire  <br> -Inexpensive  <br> -Easily integrates with PIC MCU  <br> -Very low Power | -Magnetic Sensitivity  <br> -Less output modes |
|  ![Hall Effect Sensor 3](https://github.com/user-attachments/assets/e3df8eee-b0c7-499a-b3e3-261530e28e23)     <br> -Choice 3  <br> -TLE5009  <br> -Infineon Technologies  <br> -$2.73/each  <br> -[Link](https://www.mouser.com/ProductDetail/Infineon-Technologies/TLE5009-E20102qs=%252BwNEOWq1JvGhyLjFiYi7Q%3D%3D) <br> -[Datasheet](https://www.mouser.com/datasheet/3/70/1Infineon-TLE5009_EXXXX-DataSheet-v01_01-EN.pdf) | -Low output current  <br> -Uses 3.3V and 5V | -Does not use I2C  <br> -Has more pins, harder to wire   <br> -More Expensive   <br> -Has no address |

**Rationale:** Choice 2. This Hall Effect sensor is the best option because the wiring is easy, it integrates well with the PIC, and it requires very low power. Compared to choice 3, which lacks I2C compatibility, and choice 1, which is very hard to work with.


### Table 2: Motor Driver

| Component | Pros | Cons |
|---------|------|------|
|    <img width="200" height="200" alt="image" src="https://github.com/user-attachments/assets/259d9ca6-6d01-4b70-9611-f4e3c30ed2c5" /> <br> -Choice 1 <br> -IC MTR DRV BIPLR 2.5-5.5V TSOT23 <br> 	-Monolithic Power Systems Inc. <br > -$0.83/each <br> -[Link](https://www.digikey.com/en/products/detail/monolithic-power-systems-inc/MP6513LGJ-Z/7361426) <br> -[Datasheet](https://www.monolithicpower.com/en/documentview/productdocument/index/version/2/document_type/Datasheet/lang/en/sku/MP6513LGJ-Z/)  | -Inexpensive <br> -Has CAD model <br> -Has short circuit protection | -Max Voltage supply is 5.5V <br> -Low Max Current <br> -More for small motors |
|  <img width="200" height="200" alt="image" src="https://github.com/user-attachments/assets/63ffbf3b-72db-4a41-874d-3367f02622ed" />    <br>  -Choice 2 <br>  -IC BRUSHED MOTOR DRVR 8TSSOP <br>   	-Toshiba Semiconductor and Storage <br> -$0.83/each <br> -[Link](https://www.digikey.com/en/products/detail/toshiba-semiconductor-and-storage/TB67H450AFNG-EL/15995284) <br> -[Datasheet](https://toshiba.semicon-storage.com/info/TB67H450AFNG_datasheet_en_20250730.pdf?did=70454&prodName=TB67H450AFNG) | -Inexpensive <br> -High Voltage & Current intake <br> -Has CAD file | -Only for DC brushed motors <br> -Sensitive thermal conditions  | 
|  <img width="200" height="200" alt="image" src="https://github.com/user-attachments/assets/606ccb0f-e37b-4324-836b-c4fcbfb50ea0" />  <br> -Choice 3 <br> -12-V, 1.76-A BRUSHED DC MOTOR DR <br> 	-Texas Instruments <br> -[Link](https://www.digikey.com/en/products/detail/texas-instruments/DRV8210DRLR/15286847) <br> -[Datasheet](https://www.ti.com/lit/ds/symlink/drv8210.pdf?HQS=dis-dk-null-digikeymode-dsf-pf-null-wwe&ts=1770877680405) | -Cheapest  <br> -Protection features <br> -Has CAD file | -Only for DC brushed motors <br> -Under 12V |

**Rationale:** Choice 2. This motor driver it is compatible with stepper and non stepper DC motors, and it can handle high current and voltage. While the other drivers can not supply 12V to a motor.


### Table 3: DC Motor

| Component | Pros | Cons |
|---------|------|------|
|  <img width="200" height="200" alt="image" src="https://github.com/user-attachments/assets/427120ef-6669-4ab0-9350-a32cda85099a" />  <br> -Choice 1 <br> -STANDARD MOTOR 6600 RPM 12V <br> 	-SparkFun Electronics <br> -$2.75/each <br> -[Link](https://www.digikey.com/en/products/detail/sparkfun-electronics/11696/6163657) <br> -[Datasheet](https://mm.digikey.com/Volume0/opasdata/d220001/medias/docus/951/ROB-11696_Web.pdf) | -Cheap <br> -Can intake 12V  <br> -2-wire setup | -Low torque <br> -Needs a custom footprint <br> -Little data on the datasheet |
| <img width="200" height="200" alt="image" src="https://github.com/user-attachments/assets/5d55a898-66d3-45e2-bcfa-d092ef51ee8b" /> <br> -Choice 2 <br> -GEARMOTOR 35 RPM 12V MICRO METAL <br> 	-Pololu <br> $37.95 <br> -[Link](https://www.digikey.com/en/products/detail/pololu/3046/10450048) <br> -[Datasheet](https://www.pololu.com/file/0J1487/pololu-micro-metal-gearmotors-rev-6-1.pdf) | -Uses 12V <br> -High torque <br> -2-wire connection | -High power <br> -Needs a custom footprint <br> -May be too slow |
| <img width="200" height="200" alt="image" src="https://github.com/user-attachments/assets/b3d44045-bbae-4623-bf88-854a9ccc35e4" />  <br> -Choice 3 <br> -GEARMOTOR 220 RPM 12V MICR METAL <br> -Pololu <br> -$26.45 <br> -[Link](https://www.digikey.com/en/products/detail/pololu/3042/10450044) <br> -[Datasheet](https://www.pololu.com/file/0J1487/pololu-micro-metal-gearmotors-rev-6-1.pdf) | -Steady speed <br> -2-wire connection <br> -Uses 12V | -Might be not enough torque/not fast enough <br> -May not be suitable for a drive train <br> -Needs a custom footprint |

**Rationale:** Choice 3. This motor has a good amount of speed and torque, and uses 12V, that it should be able to run our drive train well. 


### Table 4: 3.3V 1.5A Switching Power Supply
 To be determined <br>

| Component | Pros | Cons |
|---------|------|------|
| - | - | - |


### Table 5: 12V 2A AC-DC Wall Power Supply

| Component | Pros | Cons |
|---------|------|------|
| ![12V Wall Power 1](https://github.com/user-attachments/assets/851bcc5a-d03c-4438-b80b-d4cf19db04fa)     <br>  -Choice 1  <br> L6R24-120  <br> -Tri-Mag, LLC   <br> -$10.38/each   <br> -[Link](https://www.digikey.com/en/products/detail/tri-mag-llc/L6R24-120/7682639) <br> -[Datasheet](https://www.tri-mag.com/wp-content/uploads/2021/05/L6R24-L6R30_Series_2021-02.pdf) | -Inexpensive  <br> -Has less noise  <br> Average Efficiency | -The cord is short | 
|  ![12V Wall Power 2](https://github.com/user-attachments/assets/969ed2ea-2765-4eba-a302-e7469fd92a16)    <br>  -Choice 2  <br> -WSU120-2000  <br> -Triad Magnetics  <br> -$15.07 each  <br> -[Link](https://www.digikey.com/en/products/detail/triad-magnetics/WSU120-2000/3094983) <br> -[Datasheet](https://catalog.triadmagnetics.com/Asset/WSU120-2000.pdf) | -Average Efficiency  <br> -Inexpensive | -More Expensive  <br> -Has more noise |
| ![12V Wall Power 3](https://github.com/user-attachments/assets/49f281c1-7b19-4a5e-b7aa-e597b33bff10)      <br>  -Choice 3  <br> MDS-030AAC12 AB  <br> -Delta Electronics  <br> -$29.26/each  <br> -[Link](https://www.digikey.com/en/products/detail/delta-electronics/MDS-030AAC12-AB/6150232)  <br> -[Datasheet](https://psu.deltaww.com/en/products/download/Datasheet/MDS-030AAC05) | -Medical Power Supply  <br> -Average Efficiency | -Very Expensive  <br> -Big |

**Rationale:** Choice 1. This power supply has low output noise and is not too expensive. The other power supplies are around the same, but choice 2 has more noise, and choice 3 is overkill, as it is for medical devices.







