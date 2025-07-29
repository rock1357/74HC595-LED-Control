# 74HC595-LED-Control
A project demonstrating how to control 8 LEDs using the 74HC595 shift register with Arduino

## Overview
This project demonstrates how to control 8 LEDs using a 74HC595 shift register connected to an Arduino UNO. By utilizing the shift register, we can control multiple LEDs without taking up all the Arduino's digital pins.

## Components Used:
- 1 x Arduino UNO
- 1 x 74HC595 Shift Register
- 8 x LEDs
- 8 x 220Ω Resistors
- Jumper wires, breadboard

## How It Works:
- The 74HC595 shift register stores 8 bits of data, each bit controlling one LED.
- The Arduino sends serial data (one bit at a time) to the shift register, which then outputs it in parallel to control the LEDs.

## Circuit Schematic:
![Circuit Diagram](wiring_diagram.png)

## Arduino Code:
The Arduino code sends a sequence of data to the shift register, turning LEDs on one at a time. The LED sequence is as follows:

```cpp
int latchPin = 11; 
int clockPin = 9; 
int dataPin = 12;
byte leds = 0;

void setup() {
  pinMode(latchPin, OUTPUT); 
  pinMode(dataPin, OUTPUT); 
  pinMode(clockPin, OUTPUT);
}

void loop() {
  leds = 0;
  updateShiftRegister();
  delay(500); 
  for (int i = 0; i < 8; i++) { 
    bitSet(leds, i); 
    updateShiftRegister(); 
    delay(500); 
  }
}

void updateShiftRegister() {
  digitalWrite(latchPin, LOW); 
  shiftOut(dataPin, clockPin, LSBFIRST, leds); 
  digitalWrite(latchPin, HIGH);
}
