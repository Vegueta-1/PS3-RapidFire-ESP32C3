<img width="2514" height="1268" alt="Screenshot 2026-08-07 103729" src="https://github.com/user-attachments/assets/409a70d2-0f6d-459f-8dcd-f6f5dfac2a08" />

Go here to Flash it via Web https://vegueta-1.github.io/PS3-RapidFire-ESP32C3/


------------------------------------------------------------
------------------------------------------------------------
PS3 Rapid Fire for ESP32-C3  
Firmware: v0.9.36  
Author: Vegueta1  
Purpose: PS3 controller rapid-fire.

------------------------------------------------------------
Hardware Setup
------------------------------------------------------------
Recommended Starting Configuration:

33 Ω resistor: GPIO4 → GPIO3 → Controller COM 2. 
COM 2. Common Line for Analog Buttons
This is the common reference line for the analog face buttons (Square, Cross, Circle, Triangle, R1, R2).

Controller Type / Board Model	Test Point Label


Sixaxis (PP4-, PP4+)	TP18

Sixaxis (V2, V2.5)	TP26

DualShock 3 (VX, V3.5X, VX3)	TP18

DualShock 3 (VX4, VX5, VX6)	TP18

ASUKA (1.06)	T102


Important:
Do NOT replace the 33 Ω resistor with large values such as 1 kΩ or 10 kΩ.
The DRIVE line is timing-sensitive. Excessive resistance slows the signal edge and interferes with reliable button-bus operation.

------------------------------------------------------------
Default Rapid-Fire Configuration (R1/R2)
------------------------------------------------------------
Mode: OFF  
SPS: 6  
Burst: 5  
Trigger Polarity: LOW  
ADC Threshold: 40%  
Debounce: 8  
Slot Width: 500 µs  
Trigger Slot: R1 or R2  
Pulse Slot: R1 or R2  
Pulse Start: 0 µs  
Pulse Width: 500 µs  
Continuous Phase: +10 µs

------------------------------------------------------------
Web Interface
------------------------------------------------------------
After flashing and powering the ESP32-C3, connect to the Wi-Fi access point:

SSID: Ps3 Rapidfire  
Password: 12345678

Open the configuration page:

[http://192.168.4.1](http://192.168.4.1)

The firmware hosts its own web interface at 192.168.4.1.

------------------------------------------------------------
Automatic Saving
------------------------------------------------------------
All tuning parameters are saved automatically in ESP32 NVS.

Saved parameters:
Slot Width  
Trigger Slot  
Pulse Start  
Pulse Width  
Pulse Slot  
Continuous Phase  
Debounce  
ADC Threshold  
SPS  
Burst Count

Settings persist across power cycles. No manual save required.

------------------------------------------------------------
Inactivity Protection
------------------------------------------------------------
After 5 minutes:
Rapid-fire is turned OFF.  
Continuous and Burst modes disengage.  
Firing state resets.

After 15 minutes:
ESP32 enters deep sleep.  
Trigger monitor becomes the wake source.  
Reduces unnecessary power consumption.

------------------------------------------------------------
Continuous Phase
------------------------------------------------------------
Continuous Phase Offset Range: -200 µs to +200 µs  
Default: +10 µs

This shifts the continuous-fire mask relative to the pulse slot start.

Why adjust it:
Useful for testing different controller revisions or aligning simulated button activation with the controller scan window.

Recommended:
Leave at +10 µs unless tuning bus timing.

------------------------------------------------------------
Trigger Slot
------------------------------------------------------------
Defines which button-matrix slot contains the monitored trigger.

Default: R1  
Available: R2, R1

Standard configuration:
Trigger Slot = R1 or R2

------------------------------------------------------------
Pulse Slot
------------------------------------------------------------
Defines which button slot receives the rapid-fire pulse.

Default: R1
Available: R2, R1

Standard configuration:
Trigger Slot = R1 or R2  
Pulse Slot   = R1 or R2

------------------------------------------------------------
Trigger Debounce
------------------------------------------------------------
Debounce Range: 1 to 10  
1 = instant  
8 = default  
10 = heavy filtering

Lower values:
Faster trigger recognition, less filtering.

Higher values:
More filtering, slower recognition.

Recommended: 8  
Increase if trigger is noisy.  
Decrease if response feels delayed.

------------------------------------------------------------
ADC Threshold
------------------------------------------------------------
Determines how far the analog trigger must move from idle to count as pressed.

Range: 30% to 95%

Lower threshold:
More sensitive.  
Useful when trigger range is small or does not reliably reach firing point.

Higher threshold:
More strict.  
Useful when trigger fires too easily or noise causes false presses.

Tip:
Watch the live ADC reading and choose a value that clearly separates released vs pressed.

------------------------------------------------------------
Master OFF
------------------------------------------------------------
MASTER OFF disables:
Continuous Fire  
Burst Fire

Returns the controller to normal operation.

------------------------------------------------------------
------------------------------------------------------------

