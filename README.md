# mikrotik-esp-monitor
A simple project for displaying values from your MikroTik Routerboard to an OLED display connected to an ESP8266 via HTTP POST requests

# What you need:
- ESP8266 (I prefer the NodeMCU)
- I2C 128x64 OLED display
- MikroTik router
- WiFi accesspoint (or integrated WiFi in your MikroTik router)

# How it works:
- The ESP is running an HTTP server
- The MikroTik router can make POST requests via the "fetch" tool to send different values to the HTTP server on the ESP
- Then the ESP puts these values into a string array and displays these values onto the OLED display

Currently it displays the number of connected WiFi clients from CAPsMAN, the temperature and voltage input of the MikroTik routerboard but it can be easily customized.
In the bottom right corner there is a moving dot which displays that data was received in the last ~15 seconds. It is also useful for detecting if something has freezed since it is moving constantly when everything is ok.

https://user-images.githubusercontent.com/47322119/116427019-eef15280-a843-11eb-8851-6d47264c3447.mp4


# Setup:
- Import the libraries into your Arduino IDE
- Change the WiFi SSID and passphrase in the code
- Compile it and flash it onto the ESP
- Connect the Display to the ESP (SCL-D1 SDA-D2 GND-GND VCC-3V3)
- Create a new schedule in your MikroTik Router
- Paste the MikroTik_Script there
- Change the IP Address (espIP in the MikroTik Script) to the one your ESP got (make sure that your ESPs IP is static)
- Set the interval to 1 - 10 seconds (works best with 1 second interval) and enable the script.
- Now the ESP should display the variables like shown in the video above
- Feel free to modify the code to match your preferences

# Background Story:
We wanted to integrate a Mikrotik Router inside an old train that acts as a hotspot for customers. To check if everything is working I wanted to see the LTE reception, if it can connect to the internet, the bandwith usage, connected clients, GPS Location and such things. The ESP and the display will be placed directly at the drivers seat.
Originally I wanted to use the MikroTik API but since it is so complicated to use with an ESP and I didn't want to use a Raspberry Pi (because it can be corrupted easily by not powering it down properly, it will be used by non-IT people and a ESP is just faster (powering on) and cheaper) I searched for other methods and wondered if the fetch tool could also transmit data. I did a bit of research, programming, cleaning up, documenting the code and here we are now with a nice display for displaying your MikroTik stats.
