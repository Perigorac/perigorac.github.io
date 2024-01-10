
# BeeMW : an all-in-one embedded system for beehive monitoring

As students in embedded systems engineering, our school projet in late 2023 was to build a beehive monitoring system. 
## An embedded solution

BeeMW is contained withing a {DIMENSIONS} waterproof box, outfitted with many sensors to be placed in and around a beehive. These include a large metal chassis housing the weight scale, a portable camera in its separate box, and an array of wire-mounted sensors. The system is powered by a LiPo battery, one that is recharged by a solar cell, mounted with a light sensor. Thus, BeeMW can monitor three different temperatures, the hive's interior humidity, weight, interior sound, outdoor illumination, and can detect the presence of hornets with its camera.
## Low-power communications

BeeMW uses LoRaWAN, a French communication protocol, to send data over to the user. There is a LoRa antenna near the beehive array, which transmits data to a [TTN](https://www.thethingsnetwork.org/) server. Using TTN's open tools, we have developed a webhook that automatically forward data to the Dutch [BEEP](https://beep.nl/) platform, on which the data is displayed, on a variety of charts and graphs.
As the LoRa technology was designed for embedded systems, it has a low power consumption and requires a small antenna. However, it also has a low bitrate and limited airtime : this is why BeeMW only sends the most important informations possible : for example sound samples are treated locally and sent as a handful of spectral densities. Moreover, data is sent every 20 minutes.