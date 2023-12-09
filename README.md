# IntraFi Piso Wi-Fi Vendo

## Table of contents

- [IntraFi Piso Wi-Fi Vendo](#intrafi-piso-wi-fi-vendo)
  - [Table of contents](#table-of-contents)
  - [Installation](#installation)
    - [ESP Device Installation](#esp-device-installation)
  - [Configuration](#configuration)
    - [MikroTik Router Configuration](#mikrotik-router-configuration)
    - [ESP Device Configuration](#esp-device-configuration)
  - [Connection Diagram](#connection-diagram)
    - [NodeMCU ESP8266 Connection Diagram](#nodemcu-esp8266-connection-diagram)

## Installation

### ESP Device Installation

1. Download [NodeMCU PyFlasher](https://github.com/marcelstoer/nodemcu-pyflasher/releases), an EXE file for Windows, and a DMG file for MAC.
2. Download the [CH341SER](https://learn.sparkfun.com/tutorials/how-to-install-ch340-drivers/windows-710) driver for Windows only to enable communication with the `NodeMCU ESP8266` through the USB.
3. Download the latest firmware [ESP8266-firmware](https://github.com/IntraFi/PisoWiFiVendo/releases) BIN file.
4. Now open the `NodeMCU PyFlasher` and flash the firmware, see the example image below.

   ![pyflasher-win](https://github.com/IntraFi/PisoWiFiVendo/blob/main/docs/img/pyflasher-win.png?raw=true)

- Change the `Baud Rate` to the next lowest number if your Windows/MAC device is not supported.
- If you choose not to format the settings or configuration saved on the ESP device, select `no` at the `Erase Flash` section.
- Select `Flash NodeMCU` to initiate the firmware flashing process for the ESP device.

## Configuration

### MikroTik Router Configuration

1.  Perform the [ESP Device Installation](#esp-device-installation) first.
2.  No configuration needed in MikroTik device, the ESP device will do all the work.
3.  To perform the automatic configuration, see the instructions below.

    1.  Ensure that the `router has an internet connection` by connecting PORT 1 _(Internet Port)_ to the main router connected to the ISP provider.
    2.  Ensure that the router is configured with `admin` as the username and a `blank` password to enable to `start the automatic configuration`.
    3.  Connect to the ESP device setup named `INTRAFI-SETUP-ESPxxxx` Wi-Fi network after connecting a captive portal pop-up will show.

        ![intrafi-setup-wifiname](https://github.com/IntraFi/PisoWiFiVendo/blob/main/docs/img/intrafi-setup-wifiname.png?raw=true)

    4.  If there is no captive portal automatically pop-up, check your notification or open a browser and go to this URL [http://192.168.4.1](http://192.168.4.1), use the default `admin` for the password.

        ![intrafi-signin](https://github.com/IntraFi/PisoWiFiVendo/blob/main/docs/img/intrafi-signin.png?raw=true)

    5.  Scan the network first by clicking the Wi-Fi icon at the right side of the `Network Name`, then choose the network to connect.

        ![esp-wifi-settings-scan](https://github.com/IntraFi/PisoWiFiVendo/blob/main/docs/img/esp-wifi-settings-scan.png?raw=true)

    6.  Then, follow the provided instructions for the ESP Wi-Fi settings below.

        #### MikroTik Default Configuration

        If the MikroTik device has the default configuration, is likely a brand new device, or has no DPK file installed, then connect the ESP device directly to the MikroTik router's built-in Wi-Fi or through the Wi-Fi antenna.

        ![esp-wifi-settings-connect-defaultconfig](https://github.com/IntraFi/PisoWiFiVendo/blob/main/docs/img/esp-wifi-settings-connect-defaultconfig.png?raw=true)

        _The default Wi-Fi network name of the MikroTik router is `MikroTik-xxxx`._

        #### MikroTik with Configuration

        If the MikroTik device has been previously configured, proceed to the next steps.

        1.  If there is no DPK file installed, [factory reset the MikroTik](https://wiki.mikrotik.com/wiki/Manual:Reset) router's device to the default configuration.
        2.  If it has the default configurations, proceed with the steps for [MikroTik Default Configuration](#mikrotik-default-configuration), and skip the steps below.
        3.  Ensure that the MikroTik router device has the IP server list `API Enabled` with the default port 8728.

            ![ip-service-list](https://github.com/IntraFi/PisoWiFiVendo/blob/main/docs/img/ip-service-list.png?raw=true)

            _MikroTik configuration can be located at "IP -> Services"._

        4.  Ensure that the MikroTik router has given access to the ESP device, if ever a hotspot server is configured add the ESP device at the `Hotspot IP-Bindings`.

            ![hotspot-ip-bindings](https://github.com/IntraFi/PisoWiFiVendo/blob/main/docs/img/hotspot-ip-bindings.png?raw=true)

            _MikroTik configuration can be located at "IP -> Hotspot -> IP Bindings"._

        5.  Now we can connect the ESP device, through the given Wi-Fi settings.

            ![esp-wifi-settings-connect-withconfig](https://github.com/IntraFi/PisoWiFiVendo/blob/main/docs/img/esp-wifi-settings-connect-withconfig.png?raw=true)

            _Use only the `IP Address` in the Wi-Fi settings that matches to the configuration from step 4._

        #### MikroTik with IntraFi Default Configuration

        If the MikroTik device has been configured with IntraFi automatic configuration or decide to [factory reset the MikroTik](https://wiki.mikrotik.com/wiki/Manual:Reset) device, it will have the `INTRAFI-MIKROTIK-SETUP` network name if the device has built-in Wi-Fi. In such a case, proceed to the next step.

        1.  If the MikroTik device has built-in Wi-Fi, proceed to this step. Then, connect the ESP device using the Wi-Fi settings shown in the image below.

            ![esp-wifi-settings-connect-intraficonfig-builtinwifi](https://github.com/IntraFi/PisoWiFiVendo/blob/main/docs/img/esp-wifi-settings-connect-intraficonfig-builtinwifi.png?raw=true)

        2.  If the MikroTik device lacks built-in Wi-Fi but has an external antenna, connect the antenna to PORT 2 or PORT 3. Then, connect the ESP device using the Wi-Fi settings shown in the image below.

            ![esp-wifi-settings-connect-intraficonfig-withantenna](https://github.com/IntraFi/PisoWiFiVendo/blob/main/docs/img/esp-wifi-settings-connect-intraficonfig-withantenna.png?raw=true)

    7.  After completing all the steps and the `MikroTik Automatic Configuration`, the `INTRAFI-SETUP-ESPxxxx` will be hidden. If it fails and is shown again, repeat the steps, starting from Step 2. For assurance, in case the firmware is corrupted., start again from Step 1.

### ESP Device Configuration

1. Perform the [MikroTik Router Configuration](#mikrotik-router-configuration) first. If your ESP device configuration has been reset, proceed to the next steps.

2. Connect to the MikroTik router's Wi-Fi, open a browser, and navigate to the URL [http://10.0.0.2](http://10.0.0.2). Use `admin` as the default password, but only if it has not been updated.

3. Set up the `MikroTik Account`. This is crucial for using the `Piso Wi-Fi Vendo Features`. If the username or password is forgotten, the only way to recover is by [factory resetting the MikroTik](https://wiki.mikrotik.com/wiki/Manual:Reset) router's device.

   ![esp-vendoconfig-mikrotik](https://github.com/IntraFi/PisoWiFiVendo/blob/main/docs/img/esp-vendoconfig-mikrotik.png?raw=true)

4. Update the `Vendo Account`. If the password is forgotten, the only way to reset the ESP device is by pressing the `RST` button five times. The timing of the reset count is after the `first buzzer tone`, then the `built-in LED will blink five times`. During the blink, press the reset button. After that, the count will reset to zero. If the ESP device has been reset, the `INTRAFI-SETUP-ESPxxxx` Wi-Fi network will be shown and the vendo sales will not be reset.

   ![esp-vendoconfig-vendo](https://github.com/IntraFi/PisoWiFiVendo/blob/main/docs/img/esp-vendoconfig-vendo.png?raw=true)

   ![nodemcu-esp8266-resetbutton](https://github.com/IntraFi/PisoWiFiVendo/blob/main/docs/img/nodemcu-esp8266-resetbutton.png?raw=true)

   _The reset button for the NodeMCU ESP8266 device._

5. Bind the `MikroTik Portal Settings` and download the latest `MikroTik Hotspot Portal Files`. If the `MikroTik Hotspot Portal Bind` button is colored, this notifies you to update the necessary settings.

   ![esp-vendoconfig-hsportalbind-colors](https://github.com/IntraFi/PisoWiFiVendo/blob/main/docs/img/esp-vendoconfig-hsportalbind-colors.png?raw=true)

   _The quick access buttons MikroTik Hotspot Portal Bind color indicators._

   ![esp-vendoconfig-hsportalbind-warnings](https://github.com/IntraFi/PisoWiFiVendo/blob/main/docs/img/esp-vendoconfig-hsportalbind-warnings.png?raw=true)

   _The MikroTik Hotspot Portal Bind requires to update warnings._

   #### MikroTik Portal Settings Update

   Input all the required details and choose the `Vendo Rate Features` and `Hotspot Portal Features`, as shown in the image below.

   ![esp-vendoconfig-hsportalbind-settings](https://github.com/IntraFi/PisoWiFiVendo/blob/main/docs/img/esp-vendoconfig-hsportalbind-settings.png?raw=true)

   #### MikroTik Portal Files Download

   ![esp-vendoconfig-hsportalbind-files1](https://github.com/IntraFi/PisoWiFiVendo/blob/main/docs/img/esp-vendoconfig-hsportalbind-files1.png?raw=true)

   _The MikroTik Portal Files Download requires internet connection._

   ![esp-vendoconfig-hsipbinding](https://github.com/IntraFi/PisoWiFiVendo/blob/main/docs/img/esp-vendoconfig-hsipbinding.png?raw=true)

   _The Hotspot IP Binding will gain access to the internet and to the MirkoTik Web Admin Panel._

   ![esp-vendoconfig-hsportalbind-files2](https://github.com/IntraFi/PisoWiFiVendo/blob/main/docs/img/esp-vendoconfig-hsportalbind-files2.png?raw=true)

   ![esp-vendoconfig-hsportalbind-files3](https://github.com/IntraFi/PisoWiFiVendo/blob/main/docs/img/esp-vendoconfig-hsportalbind-files3.png?raw=true)

   ![esp-vendoconfig-hsportalbind-files4](https://github.com/IntraFi/PisoWiFiVendo/blob/main/docs/img/esp-vendoconfig-hsportalbind-files4.png?raw=true)

6. Update the `System Clock` since the default `NTP Pool Server` may be unreliable and take time to sync. This is crucial for verifying and determining the expiration validity of the generated vouchers and for the sales report.

   ![esp-vendoconfig-clock1](https://github.com/IntraFi/PisoWiFiVendo/blob/main/docs/img/esp-vendoconfig-clock1.png?raw=true)

   ![esp-vendoconfig-clock2](https://github.com/IntraFi/PisoWiFiVendo/blob/main/docs/img/esp-vendoconfig-clock2.png?raw=true)

7. After completing all the steps, access to the `Hotspot Portal` at [http://10.0.0.1](http://10.0.0.1) will be available. If any screens appear, follow the steps below.

   #### Hotspot Portal as MikroTik Web Admin Panel

   ![hotspotportal-mkadminpanel](https://github.com/IntraFi/PisoWiFiVendo/blob/main/docs/img/hotspotportal-mkadminpanel.png?raw=true)

   - If it was binded through the hotspot IP binding, unbind it in the ESP device `Admin Panel` at [http://10.0.0.2](http://10.0.0.2). Locate it at _Menu -> Hotspot IP Binding_, as shown in the picture above (right side).

   - If the MikroTik router's device has an antenna, it must be connected to PORT 2 or PORT 3. Otherwise, if it was connected to PORT 2, it will be displayed in the picture above (left side).

   #### IntraFi Hotspot Portal without Settings or Default Hotspot Portal

   ![hotspotportal-nosettings](https://github.com/IntraFi/PisoWiFiVendo/blob/main/docs/img/hotspotportal-nosettings.png?raw=true)

   _Hotspot portal settings are missing. Double click/tap the device information below to show the hotspot portal setup, as shown in the picture above (left side)._

   ![hotspotportal-nofiles](https://github.com/IntraFi/PisoWiFiVendo/blob/main/docs/img/hotspotportal-nofiles.png?raw=true)

   _Hotspot portal files are missing._

   - If it was previously configured for the MikroTik and ESP devices, proceed with the [ESP Device Configuration](#esp-device-configuration), starting from Step 5.

8. Enjoy earning passive income!

## Connection Diagram

#### NodeMCU ESP8266 Connection Diagram

- NodeMCU ESP8266 (ESP8266 12-E Chip; 4MB Flash Size)
- NodeMCU ESP8266 Expansion Base Board
- Buzzer
- Relay
- Coinslot
- Optional, Ethernet W5500 Module green or blue color (not yet supported!)

![intrafi-nodemcu-esp8266-wireless-and-lan-connection-diagram](https://github.com/IntraFi/PisoWiFiVendo/blob/main/docs/img/intrafi-nodemcu-esp8266-wireless-and-lan-connection-diagram.png?raw=true)
