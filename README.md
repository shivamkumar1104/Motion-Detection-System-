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


## Here's Code:-
#include <ESP8266WiFi.h>
#include <ESP8266HTTPClient.h>


const char* ssid = "REPLACE_WITH_YOUR_SSID";
const char* password = "REPLACE_WITH_YOUR_PASSWORD";

const char* server = "http://api.thingspeak.com/update";
String apiKey = "REPLACE_WITH_WRITE_API_KEY"; 

const int pirPin = D1; 
bool motionDetected = false;

void setup() {
  Serial.begin(9600);
  pinMode(pirPin, INPUT);
  connectToWiFi();
}

void loop() {
  motionDetected = digitalRead(pirPin);

  if (motionDetected) {
    Serial.println("Motion detected!");

 // Send data to ThingSpeak
    if (WiFi.status() == WL_CONNECTED) {
      WiFiClient client;         
       HTTPClient http;
      String url = String(server) + "?api_key=" + apiKey + "&field1=" + String(motionDetected);
      http.begin(client, url);     
      int httpResponseCode = http.GET();
      if (httpResponseCode > 0) {
        Serial.println("Data sent to ThingSpeak.");
      } else {
        Serial.print("Error sending data: ");
        Serial.println(httpResponseCode);
      }
      http.end();
    } else {
      
      connectToWiFi();
    }

    
    delay(5000); 
  
  }

  delay(5000);
   
  }

  delay(5000);
}
void connectToWiFi() {
  Serial.print("Connecting to WiFi");
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  Serial.println(" Connected to WiFi");
}
