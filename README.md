# Icarus-Flight-Controller

A Custom 4 layer Flight Controller Designed in Altium for a 3s-Lipo UAV

This board features a STM32F405 Microcontroller and BMI 270 IMU
Including SWD, USB-C, power protection and a 3.3V buck

Major Designs include 
- MCU/Peripheral selection
- Power regulation
- Reverse Polarity Protection
- Overcurrent Protection
- TVS Protection
- USB Communication
- SWD Programming
- IMU Integration
- Crystal/Clock Circuitry
- 4-Layer PCB
- USB differential pair routing
- DFM(Design for Manufacturing)

Architecture
3S-Lipo->Reverse Polarity Protection->Polyfuse->TVS->3.3 Buck->STM32/BMI270->USB-C, SWD, SPI, UART, PWM/GPIO

Main Components
STM32F405
Relevant Features 
- ARM Cortex-M4 Core
- multiple SPI interface
- I2C possibility
- UART
- PWM
- SWD Programming for debugging

BMI270 
- Primary IMU
- 3-axis Gyro
- 3-Axis Accelerometer
Placement of this component was paramount and kept as far away from voltage rail as possible/switching components

Power System
Used a 3S-Lipo battery
-Approx 12V

Since the voltage was meant to be stepped down from 12-3.3V it was decided that buck converter was used 
An **AP63203 buck converter** is used to step the battery voltage down to the 3.3 V rail.
- More efficient, less heat than an LDO

input protection
Reverse Polarity Protection
Used a P channel MOSFET to prevent battery / system damage 

Overcurrent Protection
Polyfuse prevents 
- Short circuits
- damaged components

Clock
- An external 8Mhz Crystal was used, as it was important for the USB - C communication which required small tolerances offers a stable system clock

PCB Design
4 Layer (Signal, GND, GND, Signal) for return path 
A multilayer design was chosen to improve:

- Ground integrity
- Power distribution
- Signal return paths
- Routing flexibility
- EMI performance
- Signal integrity

  Component placement
  Components were placed based on functional relationships rather than simply fitting them into available space
- Decoupling capacitors close to MCU power pins
- Buck-converter components grouped tightly together
- IMU positioned away from noisy switching circuitry
- USB circuitry located close to the connector
- Programming connections positioned for accessibility


Signal-integrity considerations became increasingly important as the PCB developed.
Areas considered included:

- USB differential-pair routing
- Ground return paths
- Via usage
- Trace length
- Trace spacing
- Routing near switching circuitry
- Continuous reference planes


Design for Manufacturing was another major part of the project.
The PCB was designed with fabrication constraints in mind, including:

- Minimum trace widths
- Minimum clearances
- Via sizes
- Drill sizes
- Component spacing
- Soldering accessibility
- PCB manufacturer capabilities


Final Checks were done with ERC

The development of this project was largely self directed. 
Having not previously designed a FC I had to research the components and understand the scope of the project
The process of this project generally followed the path of:
- Understand system
- Define requirements
- research components
- read datasheets
- determine architecture
- design schematic
- verify circuits
- PCB components placement
- PCB routing
- DRC

Rather than following a step by step guide a lot of the process had to do with comparing datasheets, application notes, reference designs and engineering trade offs 

Design verification
- LTSpice was used for Power rail and analog/transient behavior


What I learned
Challenge: There isnt a step by step, or a guide on what the best FC should be designed like
- Which MCU should I use?
- What peripherals are required?
- How should the board be powered?
- What protection circuitry is necessary?
- How should USB be routed?
- How should the IMU be placed?
- Which components require decoupling?
- What PCB stackup should I use?
- What manufacturing constraints should I design around?


Some of the most important lessons from the project were:
- Datasheets should drive design decisions.
- Component selection is only part of hardware design; implementation matters just as much.
- Power electronics require careful PCB layout.
- High-speed communication lines require signal-integrity considerations.
- Protection circuitry should be selected based on downstream component limitations.
- PCB placement should be based on function rather than purely geometry.
- Manufacturing limitations should be considered during the design process rather than after the PCB is completed.
- Engineering frequently requires making decisions without having a complete step-by-step solution.
