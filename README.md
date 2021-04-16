# Maxustech-MW0582TR11

MW0582TR11 is a doppler radar module from Maxustech.
It's a radar capable of detecting motion up to ~10m. The datasheet doesn't contain much information, and I haven't found much online, so here is my findings.
## Pinout
- Vin
- Gnd
- Vout
- Rx
- Tx


- Vin: 5V - 18V power
- Gnd: 0V
- Vout: a signal that is normally low (0V), but pulses high to Vin for DELAY (see below) seconds when movement is detected
- Rx and Tx are for serial communication (512000 baud). Use it to configure the module

## Configuration

Serial output on startup:
|->> Maxustech Inc,.
|->> Reaserch Support Center - Nov 2019  Ver1.1
|->> Drive MCU 76E003
|->> PA: 1  REVGAIN: 7  THRES: 30  FREQ: 0  DEBUG: 0 
|->> LIGHT:  0  DELAY:  2

Send AT commands to configure it:
AT+DELAY=0001 (0001 - 3599) (Vout ON time in seconds)
AT+PA=0001 (0001 - 0007) (Output power)
AT+DEBUG=0000 (off: 0000, on: 0002) (Debug mode)
AT+THRES:
AT+FREQ:
AT+REVGAIN:
AT+LIGHT:
The mofule responds with OK if the command was successful

Cycle power to get a print of the new settings

NOTE: Putting it in debug mode will output alot of raw data and may cause the terminal to hang.

Please let me know if you know what the LED is for, and how you control it. I tried AT+LED=0001 and AT+LED=0000 and it changed the light setting in the startup output, but nothing else...

Also check out [MaxusDev](https://github.com/MaxusDev/MWTool)
