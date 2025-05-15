# Analysis

This document aims to provide documentation on the DS-1's schematic and help you better understand whats going on.

#### Changes 
This schematic used for this project was obtained from [ElectroSmash's Boss DS1 Analysis](https://www.electrosmash.com/boss-ds1-analysis) and aims to keep the fundamental design as close to a DS1 as possible with a few minor changes and improvements.
Changes done in this design are listed below-
- Pedal uses a 3PDT switch to allow for true bypass. This reduces the circuit complexity as there is no need for complex JFET circuit.
- NJM4558L Dual OP-Amp is used instead of the traditional NJM3404A as it was more widly avaiable and cheaper, making it fit for this DIY project




## Circuit Analysis

### Power Input
![alt text](image.png)
The input stage takes consists of a simple resistor divider which generate +4.5v from our +9v input which can be used as our bias voltage.

The 100uF and 22uF capacitors are bulk capacitance that stablize the power supply lines.

Diode D1 protects againsts reverse polarity connections, in case you accidentally use the wrong power adapter.

### Input Buffer
![alt text](image-1.png)

The input buffer is a plain Emitter follow circuit. in chich input goes to the base, output is taken from the emitter and collector is tied to a fixed voltage. 

- C1 isolates the guitar pedal 
