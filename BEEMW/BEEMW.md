# BeeMW : an all-in-one embedded system for beehive monitoring

As students in embedded systems engineering, our school projet in late 2023 was to build a beehive monitoring system.  So, we came up with BEEMW.


## An embedded solution

BeeMW is contained withing a 80x360mm waterproof box, outfitted with many sensors to be placed in and around a beehive. These include a large metal chassis housing the weight scale, a portable camera in its separate box, and an array of wire-mounted sensors. The system is powered by a LiPo battery, one that is recharged by a solar cell, mounted with a light sensor. Thus, BeeMW can monitor three different temperatures, the hive's interior humidity, weight, interior sound, outdoor illumination, and can detect the presence of hornets with its camera.

## Low-power communications

BeeMW uses LoRaWAN, a French communication protocol, to send data over to the user. There is a LoRa antenna near the beehive array, which transmits data to a [TTN](https://www.thethingsnetwork.org/) server. Using TTN's open tools, we have developed a webhook that automatically forward data to the Dutch [BEEP](https://beep.nl/) platform, on which the data is displayed, on a variety of charts and graphs.
As the LoRa technology was designed for embedded systems, it has a low power consumption and requires a small antenna. However, it also has a low bitrate and limited airtime : this is why BeeMW only sends the most important informations possible : for example sound samples are treated locally and sent as a handful of spectral densities. Moreover, data is sent every 20 minutes - and in the meantime, all of the sensors aren't operating : their power is cut by the TPL5110, which is restored whenever the MKRWAN board awakes from its sleep cycle. Using Arduino's [Low Power](https://github.com/arduino-libraries/ArduinoLowPower) library, we added an even more power-efficient, clock-accurate sleep mode.

## Hardware information

Our main board was the [Arduino MKRWAN 1310](https://docs.arduino.cc/hardware/mkr-wan-1310/)
### Power
[LP753636 LiPo Accumulator](https://www.tme.eu/en/details/accu-lp753636_cl/rechargeable-batteries/cellevia-batteries/)  
[CN3065 LiPo Rider Pro](https://www.seeedstudio.com/LiPo-Rider-Pro.html)  
(in French) [SOL2W Solar Cell](https://www.gotronic.fr/art-cellule-solaire-sol2w-18995.htm)  
[TPL5110 Timer Breakout](https://www.adafruit.com/product/3435)  
Two resistors of 180kΩ and 680kΩ  
### Sensors
x2 [SEN-DHT22 Temp and Humidity Sensor](https://joy-it.net/en/products/SEN-DHT22)  
x2 [DS18B20 OneWire Temperature Probes](https://www.analog.com/en/products/ds18b20.html)  
[H40A-C3-0150 Load Cell](https://www.bosche.eu/en/scale-components/load-cells/single-point-load-cell/single-point-load-cell-h40a)  
A metallic chassis to screw the load cell on  
[Grove HX711 ADC for Load Cell](https://www.seeedstudio.com/Grove-ADC-for-Load-Cell-HX711-p-4361.html)  
[SEN0390 Outdoor Light Sensor](https://wiki.dfrobot.com/Ambient_Light_Sensor_0_200klx_SKU_SEN0390)  
[RF-MIC-160 Analogue Clip Microphone](https://www.conrad.com/en/p/renkforce-rf-mic-160-clip-speech-microphone-transfer-type-details-analogue-incl-clip-2332132.html)  
[MAX9814 Microphone Amplifier with AGC](https://www.adafruit.com/product/1713)  
A mono 3.5mm TRS socket  
[OV2640 ESP32-CAM Module](https://wiki.dfrobot.com/ESP32_CAMERA-QR_Tutorial)  
### Miscellaneous
A breadboard  
A 80x360mm waterproof box  
7 Grove connectors and cables  
### Circuitry

BeeMW is integrated on a [PCB](./bmw_pcb.cad) made with [Kicad 6.0](https://www.kicad.org/).  

### Software information

All of the code, including the main loop and BEEMW's functionalities as standalone snippets of code, are available on [this repo](https://github.com/MathisVermeren/Open-Ruche-Project-SE-Polytech2023).