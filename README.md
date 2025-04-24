
# Ultra precision current and voltage measurement system 

It's a Voltage & Current measuring device using STM32 microcontroller.



## Main Components Used

- STM32F411 Development Board 
- ST Link Debugger
- LCD display 
- I2C Module 
- Operational Amplifier – LM358P
- Voltage Regulator -  LM2596S
- Resistor ( 22K , 4.7K , 10K, 3.9K , 1K )




## Circuit Diagram 

![Screenshot 2025-04-24 212222](https://github.com/user-attachments/assets/1b247d85-6254-4534-a26c-9a80b80c046a)


## Operation

- Voltage measuring device.

This measuring device is dependent on the voltage divider principle to scale the input voltage to a level that can be safely ready by the ADC of STM32F411.

As we are building a voltage measuring device which can measure a maximum voltage of 12V, we decide on the resistor value so that when the input voltage is 12Vm the output volage will be 3.3V, which is the maximum voltage that the ADC can read. 

- Current measuring device.

A shunt resistor, which is a low-value resistor is connected in series with the load. This ensures minimal voltage drop across the resistor, avoiding significant interference with the circuit. The small voltage across the resistor is measured.  An amplifier is used to amplify this voltage for a better resolution. The ADC of the microcontroller reads the amplified voltage and calculated the current using the known resistance of the shunt. 
## Demo

https://github.com/user-attachments/assets/61e199e1-2385-4c09-8ab0-07f0f0dae34b


## Discussion

• Why do we use the STM32 Black pill development board and not the STM32 Blue pill development board? 

![Screenshot 2025-04-24 215127](https://github.com/user-attachments/assets/8d0f93d1-3edf-4fa0-a058-36b077575d61)

Why is it better to use Metal Film Resistors and not Carbon Resistors?

For the majority of modern electronic circuits, metal film resistors are the preferable option due to their greater accuracy, stability, noise performance, and dependability, particularly in 
sensitive and precise applications. Although less expensive,carbon resistors are typically less accurate and dependable, which restricts their use to less important or financially sensitive applications. The tolerance level of the resistor we use is 5% but the metal film resistor has a tolerance on 1-2%, which is more accurate. We couldn’t use metal film resistors entirely as we 
couldn’t find them in the market. 
 
• Why are we using a voltage regulator? 
 
There are no 5V power sources in the market therefore we had to use a 7.2V power source. The STM32F411 development board and the LCD display needs only 5V, so we had to use a voltage regulator to get the required voltage. 
 
• Why are we using Lm2596 buck converter as the voltage regulator? 
 
The LM2596 buck converter is chosen because it offers a combination of high efficiency, wide 
input/output range, high current capability, and built-in protections at a low cost, making it 
ideal for modern electronic systems where energy efficiency and compact design are critical. 
 
• Why are using a Shunt resistor for the current measuring circuit and not any other resistor? 
 
A shunt resistor is used instead of a standard resistor because it is specifically optimized for 
current measurement. It minimizes interference with the circuit's operation, provides accurate 
results, and ensures long-term reliability in applications where precision and stability are 
critical. 
 
• Why are we using an amplifier for the current measuring circuit? 
 
The amplifier is essential for accurately amplifying and processing small signals from the shunt 
resistor or other sources. It enables precise measurement, enhances signal quality, and ensures 
compatibility with downstream components like ADCs or controllers. 
 
• Problems we encountered during the making of the project. 
 
➢ Coding to get the right values.  
➢ Malfunctions in the equipment.  
➢ Fluctuations in the values.  
➢ Lack of resources in the market  
➢ Finding a way to display the values.

