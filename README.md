# Internet_Radio
This is a simple project of an internet radio for a senior person based on Raspberry Pi 3B. 

![Final look](https://github.com/hadato/Binary_Watch/blob/master/Top_final.PNG)

## Motivation
After a long search for an internet radio which would be suitable for a senior person struggling even with basic technology ( such as TV, dumb phone), the idea was clear. There was a need for a simple internet radio with just few buttons and a volume control. In addition, all stations had to be preinstalled so the radio would be just: Turn ON/OFF, change the station, change the volume. 

## Construction and Operation
Due to an available Raspberry Pi 3B, the choice of the main boar was simple. The radio further utilises an external USB sound card and an additional Wi-Fi module to improve both the sound quality and the Wi-Fi range. For the sound amplification, a single LM1875 with a separated powere supply is used (both channels are merged to mono).  In order to keep the compact size, but the sound quality acceptable, a small 3" full range speaker (Monacor SPX-31M) is used in a 3 l vented box. The electronics (except of the sound card and the amplifier) is nested in a separated perforated compartment for better cooling. The radio itself is controlled by 3 buttons (NEXT and PREVIOUS station, MUTE). The volume is adjusted by a potentiometer. The station number and current time are displayed on a 4x20 LCD display connected through I2C to Raspberry. To power On/Off the radio, a toggle switch with a delayed power-Off circuit is utilized. The radio is build from a 6 mm thyck plywood cutted by a LASER. 

Note: For the purposes, Raspberry Zero with an additional USB hub or an non-USB sound card would be sufficient.  

## Software
The Raspberry Pi runs Raspbian with a SSH possibility. During the start-up, a simple service radio.py based on libVLC is started. The service checks for the interrupts from the buttons and behave accordingly. In addition, information to be shown is sent over I2C to the display. If the NEXT/PREVIOUS button is pressed, the service reads next/previous station from a station list saved in an external text file (the name and the station address are hardcoded). If the power switch is toggled to position OFF, the service send a command to turn the raspberry system off. After ca. 20 s, the power is switched off by switching off a relay (delay circuit). 

## To be done
So far the station name is hardcoded and no meta data are read from the internet stations. Hence, no more information are available (song name, song duration, author, ...). The logical step is to implement the meta data read-out.
