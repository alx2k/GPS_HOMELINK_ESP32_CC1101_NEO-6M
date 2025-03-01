# DIY TESLA HOMELINK LIKE GARAGE DOOR OPENER

This project aims to create an standalone garage door opener. To do that, you will need an ESP32, a CC1101 for garage door signal transmission and a GPS module (like Neo-6M, Neo-7M or Neo-8M, although others will work). 

When you get close to the Garage door, it will automatically open. Also, there is a web portal that shows relevant information, such as distance to the locations, and it also has 8 push buttons to manually open each of the 8 codes that you can include in the code.

# DISCLAIMER

This project is in an early stage. Code might be buggy. I could send unwanted signals that trigger the door. If so, please tell me, including how it happended, so I can improve the code.

Please, for safety, plug it to a switching power source. That way, when you turn off the car, the device will also poweroff to avoid phantom garage door openings.

# Special thanks

I would like to thank simondankelmann [https://github.com/simondankelmann/Esp32-SubGhz/tree/main/Esp32/Esp32-CC1101-Standalone] (https://github.com/simondankelmann/Esp32-SubGhz/tree/main/Esp32/Esp32-CC1101-Standalone).

His project helped me develop mine. Also, I will send you back to some of his projects later in the text.

# Background

I use to own a Legacy Tesla Model 3 from 2019, and that car was sold with integrated Homelink. It was one of the things I liked more about the car. Now that I have changed my car, that is something I miss. Also, as the time of this guide, now Tesla sells it as a 355 € accessory. Sorry, but that is a lot of money for a remote control. Time for DIYing.

# Compatibility

Although this idea came from Tesla's removal of Homelink as base configuration, since this is an standalone device, it can be used in any vehicle.  

# Hardware and connections

You will need three simple things. An ESP32, a CC1101 (I would recommend you buy one with external antenna for increased range) and a GPS módule (my recomendation would be a Neo-M8, BN-880 or similar. Please buy from a legitimate source, there are counterfaits on the internet using worse GPS chips, and therefore your signal will not be as accurate, and it will take longer to triangulate your position). 

For this project I am using an 8 pin CC1101, so the connections below refers to that module.

| ESP32 | CC1101 | NEO-8M |
| ----- | ----- | ----- |
| GND | 1 | GND |
| 3,3V | 2 | VCC |
| 12 | 3 | |
| 5 | 4 | |
| 10 | 5 | |
| 23 | 6 | | 
| 19 | 7 | |
| | 8 | |
| 16 | | TXD |
| 17 | | RXD |


# WHAT PARTS OF THE CODE DO YOU HAVE TO CHANGE

You will need to change the Wifi SSID and Password. Please, use a strong password.

That is mandatory. Again. THAT IS MANDATORY.

I don't want to hear that someone got robbed because a thief connected to this project default password and opened the door via the webportal. Don't be a fool please!

After that, you will need to change the remote control information:

Example:
////////////////////////////////////////////////////////////////
// ADDRESS 6: 
// DESCRIPTION: 
String location6 = "Buckingham Palace";
const double targetLat6 = 51.50142064413959;
const double targetLon6 = -0.14164269166884363;
#define LENGTH_SAMPLES_SIGNAL_6 3576
#define FREQUENCY_SIGNAL_6 433.92
int samples_signal_6[LENGTH_SAMPLES_SIGNAL_6] = {};

In this part of the code, you will need to change the location name. This name will be used for Log output and also for the name that appears in each of the 8 push buttons in the web portal.

TargetLat and TargetLon are the GPS latitude and longitude of each of the garage doors. The simplest way to obtain this is Google Maps. Go to the location, right click and you will see the latitude and longitude in the first way of the popup menu. If you click on it, the location is copied and you can paste it into the code.

LENGTH_SAMPLES_SIGNAL, FREQUENCY_SIGNAL AND samples_signal are the three values needed to send the correct remote signal. You will need to obtain that from the original remote.
