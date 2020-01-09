# PlatformIO ESP-IDF example with WIFI and NAT setup
The [esp-idf-nat-example](https://github.com/jonask1337/esp-idf-nat-example) ESP-IDF project wrapped in a PlatformIO project.

An example firmware to use the ESP32 as WiFi repeater.

**Requires** this lwIP library with NAT support to be used as ESP-IDF lwIP component: https://github.com/jonask1337/esp-lwip

The PlatformIO [espidf-blink](https://github.com/platformio/platform-espressif32/tree/develop/examples/espidf-blink) example project was used as 
template. 

Tested with PlatformIO for VSCode using ESP-IDF version: *framework-espidf 3.30300.190916 (3.3.0)*

## Get Started
The following are the steps required to run this project on the ESP32 and turn it into a WiFi repeater.

### Step 1 - Get lwIP library with NAT 
Download the repository of the NAT lwIP library using the following command:

`git clone https://github.com/jonask1337/esp-lwip.git`

Note: It is important to clone the repository. If it is only downloaded it will be replaced by the orginal lwIP library during the build.
### Step 2 - Replace original ESP-IDF lwIP library with NAT lwIP library
The ESP-IDF used by PlatformIO can be found at:
- Linux: `~/.platformio/packages/framework-espidf/`
- Windows: `C:\Users\{YOUR_USERNAME}\.platformio\packages\framework-espidf\`

Go to this folder and follow these steps:

1. Rename or delete the *framework-espidf/component/lwip/lwip* directory which contains the files of the original lwIP library.
2. Copy the lwIP library with NAT repository folder you cloned in Step 1 to *framework-espidf/component/lwip/*
3. Rename the lwIP library with NAT repository folder from *esp-lwip* to *lwip*.

### Step 3 - Get the esp-idf-nat-example-pio project
Download the esp-idf-nat-example-pio project using the following command:

`git clone https://github.com/jonask1337/esp-idf-nat-example-pio.git`

### Step 4 - Configure the project
Adjust the WiFi settings in the `src/main.c` file. (see Configuration section below)

Now you can build and flash the project using the [PlatformIO](https://platformio.org/) toolchain.
If the lwIP library with NAT is used correctly by the ESP-IDF and the NAT feature is enabled you should see 
a *NAT is enabled* message in the output log of the ESP32.

## Configuration
You may have to make some changes to the *platformio.ini* file depending on your setup and what ESP32 board you are using. 

In the `src/main.c` file change the values of the *EXAMPLE_ESP_WIFI_SSID* and *EXAMPLE_ESP_WIFI_PASS* defines to the credentials
of the WIFI network the ESP32 should connect to.

With the *ESP_AP_SSID* and *ESP_AP_PASS* defines you can change the credentials of the Access Point created by the ESP32.

By Default the DNS-Server which is offerd to clients connecting to the ESP32 AP is set to 8.8.8.8.
Replace the value of the *MY_DNS_IP_ADDR* with your desired DNS-Server IP address (in hex) if you want to use a different one.
