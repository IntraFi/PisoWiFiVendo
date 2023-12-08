# IntraFi Piso Wi-Fi Vendo

## Table of contents

- [IntraFi Piso Wi-Fi Vendo](#intrafi-piso-wi-fi-vendo)
  - [Table of contents](#table-of-contents)
  - [Installation](#installation)
    - [ESP Device Installation](#esp-device-installation)
  - [Configuration](#configuration)
    - [MikroTik Router Configuration](#mikrotik-router-configuration)

## Installation

### ESP Device Installation

1. Download [NodeMCU PyFlasher](https://github.com/marcelstoer/nodemcu-pyflasher/releases), an EXE file for Windows, and a DMG file for MAC.
2. Download the driver [CH341SER](https://learn.sparkfun.com/tutorials/how-to-install-ch340-drivers/windows-710) for Windows only.
3. Download the latest firmware [ESP8266-firmware](https://github.com/IntraFi/PisoWiFiVendo/releases) BIN file.
4. Now open the `NodeMCU PyFlasher` and flash the firmware, see the example image below.

![pyflasher-win](https://github.com/IntraFi/PisoWiFiVendo/blob/main/docs/img/pyflasher-win.png?raw=true)

- Change the `Baud Rate` to the next lowest number if your Windows/MAC device is not supported.
- If you choose not to format the settings or configuration saved on the ESP device, select `no` at the `Erase Flash` section.
- Select `Flash NodeMCU` to start flashing the firmware for your ESP device.

## Configuration

### MikroTik Router Configuration

1.  Perform the [ESP Device Installation](#esp-device-installation) first.
2.  No configuration needed in MikroTik device, the ESP device will do all the work.
3.  To perform the automatic configuration, see the instructions below.

    1.  Ensure that the `router has an internet connection` by connecting PORT 1 _(Internet Port)_ to the main router connected to the ISP provider.
    2.  Ensure that the router is configured with `admin` as the username and a `blank` password to enable to `start the automatic configuration`.
    3.  Connect to the ESP device setup named `INTRAFI-SETUP-ESPxxxx` Wi-Fi network after connecting a captive portal pop-up will show.

        ![intrafi-setup-wifiname](https://github.com/IntraFi/PisoWiFiVendo/blob/main/docs/img/intrafi-setup-wifiname.png?raw=true)

    4.  If there is no captive portal automatically pop-up, check your notification or open a browser and go to this URL `http://192.168.4.1`, use the default `admin` for the password.

        ![intrafi-signin](https://github.com/IntraFi/PisoWiFiVendo/blob/main/docs/img/intrafi-signin.png?raw=true)

    5.  Scan the network first by clicking the Wi-Fi icon at the right side of the `Network Name`, then choose the network to connect.

        ![esp-wifi-settings-scan](https://github.com/IntraFi/PisoWiFiVendo/blob/main/docs/img/esp-wifi-settings-scan.png?raw=true)

    6.  Then, follow the provided instructions for the ESP Wi-Fi settings below.

        #### MikroTik Default Configuration

        If the MikroTik device has the default configuration, is likely a brand new device, or has no DPK file installed, then connect the ESP device directly to the MikroTik router's built-in Wi-Fi or through the Wi-Fi antenna.

        ![esp-wifi-settings-connect-defaultconfig](https://github.com/IntraFi/PisoWiFiVendo/blob/main/docs/img/esp-wifi-settings-connect-defaultconfig.png?raw=true)

        _The default configuration of the MikroTik router's Wi-Fi network name has `MikroTik-xxxx`_

        #### MikroTik with Configuration

        If the MikroTik device has been previously configured, proceed to the next steps.

        1.  If there is no DPK file installed, reset the MikroTik router to the default configuration, indicating that it is likely a brand new device with its default configurations.
        2.  If it has the default configurations then follow the step for [MikroTik Default Configuration](#mikrotik-default-configuration). Otherwise follow the next steps.
        3.  Ensure that the MikroTik router device has IP server list `API Enabled` with a default Port 8728

            ![ip-service-list](https://github.com/IntraFi/PisoWiFiVendo/blob/main/docs/img/ip-service-list.png?raw=true)

            _MikroTik configuration can be found at IP -> Services_

        4.  Ensure that the MikroTik router has given access to the ESP device, if ever a hotspot server is configured add the ESP device at the `Hotspot IP-Bindings`.

            ![hotspot-ip-bindings](https://github.com/IntraFi/PisoWiFiVendo/blob/main/docs/img/hotspot-ip-bindings.png?raw=true)

            _MikroTik configuration can be found at IP -> Hotspot -> IP Bindings_

        5.  Now we can connect the ESP device, through the given Wi-Fi settings.

            ![esp-wifi-settings-connect-withconfig](https://github.com/IntraFi/PisoWiFiVendo/blob/main/docs/img/esp-wifi-settings-connect-withconfig.png?raw=true)

            _Use only the `IP Address` in the Wi-Fi settings that matches the configuration from step 4_

        #### MikroTik with IntraFi Default Configuration

        If the MikroTik device has been configured with IntraFi automatic configuration or decide to factory reset the device, it will have the `INTRAFI-MIKROTIK-SETUP` network name if the device has built-in Wi-Fi, then continue to the next step.

        1.  If the MikroTik device has built-in Wi-Fi, proceed to this step. Then, connect the ESP device using the Wi-Fi settings shown in the image below.

            ![esp-wifi-settings-connect-intraficonfig-builtinwifi](https://github.com/IntraFi/PisoWiFiVendo/blob/main/docs/img/esp-wifi-settings-connect-intraficonfig-builtinwifi.png?raw=true)

        2.  If the MikroTik device lacks built-in Wi-Fi but has an external antenna, connect the antenna to PORT 2 or PORT 3. Then, connect the ESP device using the Wi-Fi settings shown in the image below.

            ![esp-wifi-settings-connect-intraficonfig-withantenna](https://github.com/IntraFi/PisoWiFiVendo/blob/main/docs/img/esp-wifi-settings-connect-intraficonfig-withantenna.png?raw=true)