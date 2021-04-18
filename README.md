# Maxustech-MW0582TR11

MW0582TR11 is a 5.8GHz doppler radar module from Maxustech.
It's a radar capable of detecting motion up to ~10m. The datasheet doesn't contain much information, and I haven't found much online, so here is my findings.
## Pinout
- Vin: 5V - 18V power
- Gnd: 0V
- Vout: a signal that is normally low (0V), but pulses high to Vin for DELAY (see below) seconds when movement is detected
- Rx and Tx are for serial communication (512000 baud). Use it to configure the module

## Configuration

Serial output on startup:
```
|->> Maxustech Inc,.
|->> Reaserch Support Center - Nov 2019  Ver1.1
|->> Drive MCU 76E003
|->> PA: 1  REVGAIN: 7  THRES: 30  FREQ: 0  DEBUG: 0 
|->> LIGHT:  0  DELAY:  2
```

Send AT commands to configure it:
- AT+PA=0000 (0000 - 0007) Radiated power. The bigger the number, the more radiated power.
- AT+REVGAIN=0000 (0000 - 0007). Receive gain. The bigger the number, the more sensitive the receiver is.
- AT+DELAY=0001 (0001 - 3599) (seconds). Time delay. How long Vout is high after an object is detected.
- AT+DEBUG=0000 (off: 0000, on: 0002). Debug mode. Prints raw radar data.
- AT+THRES=0001 (0001 - 0099) Threshold. How easy the device should trigger detection. The lower the number, the device is more inclined to trigger detection
- AT+FREQ= () Frequency. Probably the radiated frequency in the range the device is capable of
- AT+LIGHT= () Light. Apparently the diode in the front is a photosensor which can be used to trigger the device only in the dark.

The module responds with OK if the command was successful

Cycle power to get a print of the new settings

NOTE: Putting it in debug mode will output alot of raw data and may cause the terminal to hang.

Also check out [MaxusDev](https://github.com/MaxusDev/MWTool)
