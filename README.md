# Self-Sorting Dustbin

A touch-free Arduino smart dustbin prototype. An ultrasonic sensor detects a person or an object at the opening, and a servo steers the waste to one of two sides depending on the humidity reading from a DHT11 sensor.

![Prototype](Project%20Pic.png)

## Why

People often mix wet and dry waste, and touching a bin lid spreads germs. This prototype explores a bin that opens without touch and separates waste automatically.

## How it works

1. The HC-SR04 ultrasonic sensor measures the distance in front of the opening.
2. If something is closer than **10 cm**, the Arduino reads the DHT11 humidity.
3. The servo moves according to the humidity reading:
   - **64% or below** → servo to 0° (dry side)
   - **65% or above** → servo to 180° (wet side)
4. When nothing is detected, the servo returns to 90° (neutral).
5. Temperature, humidity and soil-moisture values are printed on the Serial Monitor at 9600 baud.

The humidity thresholds depend on the room. Adjust them in the code (`DHT.humidity <= 64` and `>= 65`) for your environment.

## Circuit

![Circuit diagram](Circuit_Dustbin.png)

The circuit is also available as a Fritzing file: `Circuit_Dustbin.fzz`.

## Hardware

- Arduino Uno
- HC-SR04 ultrasonic sensor
- Servo motor (sorting flap)
- DHT11 temperature and humidity sensor
- Soil-moisture sensor (reading is printed only; it is not used in the sorting decision)
- 2 LEDs (shown in the circuit diagram; not driven by the current code)

## Software

- Arduino IDE
- Libraries: `Servo`, `dht` (DHT11 library)

## Setup

1. Wire the components as shown in the circuit diagram.
2. Install the `dht` library in the Arduino IDE.
3. Upload `Code_self-sorting_dustbin.ino` to the Arduino.
4. Open the Serial Monitor at 9600 baud to see the sensor readings.

## Limitations

- The sorting decision is based on **air humidity**, which is a rough stand-in for wet or dry waste. It cannot identify materials.
- The soil-moisture sensor is read but not used, and the LEDs are not controlled by the code.
- The thresholds need manual tuning for each location.
- Prototype built from cardboard; not intended for real waste handling.

## Possible improvements

- Use the soil-moisture reading in the sorting decision
- Separate the lid control (touch-free opening) from the sorting servo
- Add a fill-level sensor and an LED or buzzer indicator
- Add more waste categories

## License

Apache-2.0
