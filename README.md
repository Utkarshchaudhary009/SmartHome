# Automated Light and Door Control System

## Description
This project uses an Arduino to automate light control based on ambient light levels and door control based on proximity using an ultrasonic sensor.

## Materials Required
- Arduino board
- LDR (Light Dependent Resistor)
- Ultrasonic Sensor (HC-SR04)
- LED
- Servo Motor
- Jumper wires
- Resistor (10k ohms)
- Current-limiting resistor (330-470 ohms)

## Precautions
- Ensure proper polarity when connecting components.
- Power off the Arduino before making any circuit connections.
- Avoid short circuits by double-checking connections.
- Be cautious with the servo motor movement.

## Procedure
### Code
1. Use the provided Arduino code to control the light and door.
2. Adjust thresholds, servo positions, and timing in the code based on project requirements.

### Circuit Connection
1. Connect the LDR to A0, including a 10k ohm resistor to ground.
2. Connect the Ultrasonic Sensor's trig pin to digital pin 2 and echo pin to digital pin 3.
3. Connect the LED to digital pin 9 with a current-limiting resistor to ground.
4. Connect the Servo Motor to digital pin 10.

### Power Supply
- Power the Arduino board using an external power source or USB cable.

## Learning Outcomes
- Understanding Arduino programming for sensor-based projects.
- Implementing control logic for light and servo motor based on sensor inputs.
- Gaining experience in interfacing different electronic components.

## Engineering Required
- Basic knowledge of Arduino programming.
- Understanding analog and digital sensor interfacing.
- Familiarity with servo motor control.

## Real-Life Applications
- Home automation systems for energy efficiency.
- Security systems with automated door control based on proximity.
- Adaptive lighting systems for comfort and energy savings.
