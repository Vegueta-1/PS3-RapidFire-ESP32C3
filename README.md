⚠️ Important Notes. Online Play at your own risk! This release is provided as is, with no warranty or guarantee of fitness for any purpose. In online environments may result in bans, account suspension, or other penalties. You are solely responsible for how you use this project.


<img width="1910" height="1080" alt="PS3 Rapid-fire for ESP32-C3 - v0 9 38 - Button Deep Sleep" src="https://github.com/user-attachments/assets/751c4b38-44a2-4f25-8fc9-ac2ac578d57a" />


Video Preview: https://youtube.com/shorts/ZO7j1c5WOlM

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

<img width="800" height="537" alt="esp32-c3-super-mini-Wiring Diagram Board_VX6_0 05" src="https://github.com/user-attachments/assets/5c87ee29-4471-4197-8624-593b1978550b" />




                 33 Ω
    GPIO4 ────────/\/\/\/\/────────┬──────────── GPIO3
                                  │
                                  │ (Trace/Connection)
                                  │
                                  ▼
                                COM 2

33 Ω resistor: GPIO4 → GPIO3 → COM 2. Common Line for Analog Buttons
This is the common reference line for the analog face buttons (Square, Cross, Circle, Triangle, R1, R2).

Controller Type / Board Model	Test Point Label

<img width="1155" height="1127" alt="Controller Board Mode test Point Label" src="https://github.com/user-attachments/assets/7b5d28ea-36fe-4ef7-8c07-a1e774693261" />






Important:
Do NOT replace the 33 Ω resistor with large values such as 1 kΩ or 10 kΩ.
The DRIVE line is timing-sensitive. Excessive resistance slows the signal edge and interferes with reliable button-bus operation.
Very Important remember that always connect the Ground from Esp32 C3 to the Controller Ground!
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

 SHUTDOWN ESP32-C3
⚠ To sleep: Press and hold the button on GPIO1 for 6 seconds, then release. OR use the Web UI button.
To wake: Press the button (any duration) – device wakes instantly.
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

