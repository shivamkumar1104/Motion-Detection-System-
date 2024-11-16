# Motion-Detection-System-
Motion Detection System that uses sensors and other components to detect movement in a specified area. It is  a useful system for security and monitoring applications, alerting when any motion is detected.

## Components
1. PIR Sensor: Detects movement by sensing infrared radiation.
2. Microcontroller (NodeMCU ESP8266): Processes sensor data and controls the output devices.
3. Jumper Wires and USB cable.
4. Power supply (USB cable).
5. A ThingSpeak account (free registration).

## Setup Instructions

 Hardware Setup
1. Connect the PIR sensor to the NodeMCU:

-> VCC pin to 3.3V on NodeMCU.
->GND pin to GND on NodeMCU.
->Output pin to a GPIO pin (e.g., D1).

2. Power the NodeMCU using a USB cable or an appropriate battery.

Software Setup
1. Install Arduino IDE and configure it for ESP8266 development:

->Add the ESP8266 board manager URL:     http://arduino.esp8266.com/stable/package_esp8266com_index.json
->Install the ESP8266 Board Package.

2. Install Required Libraries:

->ESP8266WiFi
->ThingSpeak

3. ThingSpeak Setup:

->Create a ThingSpeak channel.
->Note down the Write API Key from the channel settings.

4. Arduino Code:

->Download the motion_detection.ino file from this repository.
->Open the file in Arduino IDE.
