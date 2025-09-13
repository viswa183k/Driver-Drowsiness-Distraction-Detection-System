# Driver_Drowsiness_Detection

## Description
Edge-AI driver monitoring system: Raspberry Pi camera + MediaPipe detects eye closure and yawns (drowsiness). Pi sends alerts over serial to an Arduino with MCP2515 CAN module for vehicle/CAN alerts and local buzzer/LED warning. Optional ThingSpeak logging.

## Hardware Required
- Raspberry Pi 3/4 (or Jetson Nano) + Pi Camera or USB webcam
- Arduino Uno/Mega (or compatible)
- MCP2515 CAN module (SPI) connected to Arduino
- Buzzer and LED(s)
- USB serial cable between Pi and Arduino
- (Optional) NEO-6M GPS or OBD-II CAN interface for richer data

## Software Required
- On Pi: Python3, OpenCV, MediaPipe, pyserial, requests
  - Install: `pip3 install opencv-python mediapipe pyserial requests`
- On Arduino: MCP_CAN library (e.g., https://github.com/coryjfowler/MCP_CAN_lib)
- ThingSpeak account (optional) for logging alerts

## Wiring Summary
- MCP2515 CS -> Arduino D10 (adjust in .ino)
- MCP2515 SPI -> Arduino SPI pins (MOSI/MISO/SCK)
- Buzzer -> Arduino D8, LED -> D7 (changeable)
- Pi camera -> Raspberry Pi
- Pi USB -> Arduino Serial (or use UART pins with level shifting)

## Usage
1. Upload `Driver_Drowsiness_Detection.ino` to Arduino (install MCP_CAN lib).
2. Put Python file on Pi: `pi/driver_monitor.py`. Edit SERIAL_PORT and THINGSPEAK key.
3. Boot Pi, `python3 driver_monitor.py`. Grant camera permissions.
4. On detection, Pi sends "DROWSY" over serial; Arduino triggers alerts and sends CAN frames.
5. Tune EAR_THRESHOLD, MAR_THRESHOLD, and consecutive frame counts for reliability.

## Safety & Testing
- Test system stationary first.
- Tune thresholds in daylight & night conditions.
- This is a safety-assist prototype — do not rely solely on it in real-world driving without robust validation.

## Author
K. Viswanadh
