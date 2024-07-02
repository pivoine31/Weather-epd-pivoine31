L.Marzen ESP32 Weather EPD station software with additional features 

Based on https://github.com/lmarzen/esp32-weather-epd (source code retrieved on 27/06/2024) 

This repository contains an update of the Luke Marzen ESP32 Weather station software, adding some interesting features:
- Wi-Fi handling several networks / credentials
- Embedded Web server (for managing Wi-Fi credentials, Geographic locations for displaying weather, weather station general parameters)
- Automatic switching of the precipitation display pattern to avoid the contrast problem (the threshold may be modified trough the Web pages)
  The contrast modification in itself was submitted by dwuhls on issue #62 "eink display loses contrast on days with high PoP"
- A feature named POP_AND_VOL that allows displaying simultaneously the probability of precipitations and the volume of precipitations (hourly and daily)

In the modified code, most of the customization options are moved to config.h

Using the Web server requires to identify a means for waking-up the station in web server mode: by default, this is triggered by hitting the internal button

Others alternatives are:
- using a touch pin connected to a metallic thing accessible from the outside (probably the best alternative when the internal button is not accessible)
- using a custom button other than the internal one (connected with a pullup resistor to the esp32)

Once the Web server is started, a specific icon is displayed in the upper left corner and the Web pages may be acceeded using the IP of the station as URL (HTTP, because HTTPS not supported for this purpose)
The Web server terminates itself after 3 min without activity (by default), or when the button is pressed again, through "exit" on Web pages

If not interested by the Web server, there is a custom option in config.h to disable it (#undef WEB_SVR, or remove, or comment)
Doing this, you may still enable the "automatic pop switch", and the "pop and vol" features

This software remix does no longer need tuning the TIMEZONE and using NTP for time synchronization since the OWM service responses provides both the time information and the time offset relative to GMT based on the selected geographic location (lat/lon)

Otherwise, config.h may be customized as usual, relying on the indications found in comments
