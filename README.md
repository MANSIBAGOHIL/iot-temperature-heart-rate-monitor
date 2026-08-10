# iot-temperature-heart-rate-monitor
Arduino and IoT prototype that measures temperature and pulse rate, displays readings on a 16x2 LCD, and sends data to ThingSpeak through an ESP8266-01.

# Temperature and Heart Rate Monitoring Prototype

An Arduino-based prototype that reads body-temperature and pulse-sensor signals, displays the results on a 16x2 LCD, and sends the readings to ThingSpeak through an ESP8266-01 Wi-Fi module.

> This was an academic sensor-interfacing project. It is an educational prototype, not a calibrated or approved medical device.

## Technologies and Components

- Arduino Uno
- Arduino/C++
- ESP8266-01 Wi-Fi module
- ThingSpeak
- LM35 temperature sensor
- Optical pulse sensor
- 16x2 LCD
- `LiquidCrystal` library
- `SoftwareSerial` library
- Breadboard, jumper wires, resistors, and LED

## Features

- Samples an LM35 temperature sensor through an analog input
- Detects heartbeats and calculates beats per minute (BPM)
- Displays BPM and temperature on a 16x2 LCD
- Shows pulse information through the Arduino Serial Monitor
- Sends temperature and pulse values to two ThingSpeak fields through the ESP8266-01
- Blinks/fades an LED in response to detected beats

## How the Prototype Works

The LM35 produces an analog voltage related to temperature. The Arduino reads that signal on analog pin `A1`, converts it to a temperature value, and displays the result in Fahrenheit.

The optical pulse sensor is connected to analog pin `A0`. The program samples the signal using a Timer2 interrupt, identifies peaks and troughs, calculates the inter-beat interval, and averages recent intervals to estimate BPM.

The LCD displays both readings. The ESP8266-01 communicates with the Arduino through software serial and sends the values to ThingSpeak using an HTTP update request.

## Build Process

1. We studied the operating principles and pin requirements of the LM35, pulse sensor, and ESP8266-01.
2. We connected both sensors to the Arduino and added the LCD for local output.
3. We implemented pulse sampling and BPM calculation using timed interrupts.
4. We converted the LM35 analog reading into a temperature value.
5. We configured the ESP8266-01 with AT commands and sent temperature and pulse readings to ThingSpeak.
6. We compared the LCD, serial, and cloud outputs while troubleshooting wiring, baud-rate, display-contrast, and API-key issues.

## Running the Project

### Before you begin

Create a ThingSpeak channel with two fields:

- Field 1: temperature
- Field 2: pulse/BPM

Replace the placeholders in the sketch with your own values:

```cpp
String apiKey = "YOUR_THINGSPEAK_WRITE_API_KEY";
String wifiName = "YOUR_WIFI_NAME";
String wifiPassword = "YOUR_WIFI_PASSWORD";
```

Never commit real Wi-Fi passwords or API keys.

### Steps

1. Install the Arduino IDE.
2. Recreate the circuit using `images/schematic.png` and the original report.
3. Open `code/temperature_heart_rate_monitor.ino`.
4. Add your Wi-Fi and ThingSpeak configuration without committing the credentials.
5. Select the Arduino Uno and the correct serial port.
6. Compile the sketch and resolve any issues introduced while extracting it from the PDF.
7. Upload the sketch.
8. Open the Serial Monitor at the baud rate used by the program.
9. Place the pulse sensor on a fingertip or earlobe and observe the LCD, serial output, and ThingSpeak channel.

## What We Learned

- How to combine readings from two sensors in one Arduino project
- How pulse peaks and inter-beat intervals can be used to estimate BPM
- How to show sensor data locally on an LCD and remotely through an IoT service
- Why matching serial baud rates matters during debugging
- Why sensor voltage limits, wiring, LCD contrast, and the correct ThingSpeak write key must be checked carefully
- How to troubleshoot hardware and software together

## Limitations and Possible Improvements

- Rebuild, compile, and validate the extracted source code
- Remove hard-coded credentials and use a separate untracked configuration file
- Add exact wiring tables and verified power-level details, especially for the 3.3 V ESP8266-01
- Add timestamps and more reliable retry/error handling for network updates
- Compare readings with calibrated instruments and report error values
- Improve signal filtering and motion-artifact handling for pulse readings
- Add an enclosure and safer sensor placement
- Clearly separate educational output from medically validated measurements

## Contributors

- Mansiba Gohil
- Nidhi Dhinoja
- Hitesh Jethava
