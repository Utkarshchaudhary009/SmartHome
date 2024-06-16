
# Automated Light and Door Control System <a href="https://github.com/Utkarshchaudhary009/SmartHome/blob/main/License.md"><img src="https://img.shields.io/badge/License-MIT-yellow.svg" Alt="MIT License"></a>

## Table of Contents

  - [Description](#description)
  - [Materials Required](#materials-required)
  - [Precautions](#precautions)
  - [Procedure](#procedure)
    - [Code](#code)
    - [Circuit Connection](#circuit-connection)
  - [Power Supply](#power-supply)
  - [Learning Outcomes](#learning-outcomes)
  - [Engineering Required](#engineering-required)
  - [Real-Life Applications](#real-life-applications)


## Description

This project utilizes an Arduino to automate light control based on ambient light levels and door control based on proximity using an ultrasonic sensor.

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

```bash
#include <Servo.h>

const int ldrPin = A0;         // LDR analog pin
const int ldrDigitalPin = 4;   // LDR digital pin
const int ledPin = 9;          // LED pin
const int trigPin = 2;          // Ultrasonic sensor trigger pin
const int echoPin = 3;          // Ultrasonic sensor echo pin
const int buzzerPin = 8;       // Buzzer pin
const int servoPin = 6;        // Servo motor pin

Servo doorServo;

const float distanceThreshold = 0.5;  // Distance threshold for door opening in meters
const int buzzerDuration = 1000;      // Buzzer duration in milliseconds

bool doorOpen = false;  // Variable to track whether the door is open

void setup() {
  Serial.begin(9600);  // Initialize Serial Monitor
  pinMode(ldrDigitalPin, INPUT);
  pinMode(ledPin, OUTPUT);
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(buzzerPin, OUTPUT);
  doorServo.attach(servoPin);
}

void loop() {
  int ldrValue = analogRead(ldrPin);
  int ldrDigitalValue = digitalRead(ldrDigitalPin);

  if (isPersonNear()) {
    if (!doorOpen) {
      openDoor();
      delay(1000);  // Allow time for the door to open
      digitalWrite(buzzerPin, HIGH);  // Activate buzzer
      delay(buzzerDuration);
      digitalWrite(buzzerPin, LOW);
      doorOpen = true;  // Update the door status
      Serial.println("Door opened");
    }
  } else {
    digitalWrite(buzzerPin, LOW);
    if (doorOpen) {
      closeDoor();
      doorOpen = false;  // Update the door status
      Serial.println("Door closed");
    }
  }

  if (isDaytime(ldrValue)) {
    digitalWrite(ledPin, HIGH);  // Turn on the light during daytime
    Serial.println("Daytime");
  } else {
    digitalWrite(ledPin, LOW);   // Turn off the light during nighttime
    Serial.println("Nighttime");
  }

  delay(500);  // Delay for stability and to avoid excessive Serial output
}

bool isDaytime(int ldrValue) {
  return ldrValue > 500;  // You may need to adjust this threshold based on your environment
}

bool isPersonNear() {
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  long duration = pulseIn(echoPin, HIGH);
  float distance = (duration * 0.0343) / 2;  // Calculate distance in meters

  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" meters");

  return distance < distanceThreshold;
}

void openDoor() {
  doorServo.write(90);  // Assuming 90 degrees is the open position, adjust as needed

  // Buzzer pattern while opening the door
  for (int i = 0; i < 5; i++) {
    digitalWrite(buzzerPin, HIGH);
    delay(1000);  // Buzzer on for 1000 milliseconds
    digitalWrite(buzzerPin, LOW);
    delay(50);     // Buzzer off for 50 milliseconds
  }
}

void closeDoor() {
  doorServo.write(0);   // Assuming 0 degrees is the closed position, adjust as needed
  delay(1000);          // Allow time for the door to close
}

```

### Circuit Connection

**Ultrasonic Sensor**
- Connect the Ultrasonic Sensor's trig pin to digital pin 2 and echo pin to digital pin 3.
- VCC: Connect to Arduino 5V
- GND: Connect to Arduino GND
- Trig: Connect to Arduino Pin 2
- Echo: Connect to Arduino Pin 3

**Servo Motor**
- Connect the Servo Motor to digital pin 10.
- Signal: Connect to Arduino Pin 6
- Power: Connect to Arduino 5V
- Ground: Connect to Arduino GND

**LDR Module**
- Connect the LDR to A0, including a 10k ohm resistor to ground.
- Analog Pin: Connect to Arduino A0
- Digital Pin: Connect to Arduino Pin 4

**Buzzer**
- Connect to Arduino Pin 8

**LED**
- Connect the LED to digital pin 9 with a current-limiting resistor to ground.
- Connect to Arduino Pin 9

## Power Supply

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
