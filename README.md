# Software prerequisites
* Segger Embedded Studio for ARM (SES).
  Tested with [v4.12](https://www.segger.com/downloads/embedded-studio/Setup_EmbeddedStudio_ARM_v412_win_x64.exe),
  all versions are available [here](https://www.segger.com/downloads/embedded-studio/).
  At some point after launch, it will request a license. Fortunately, it's free for nRF development - just fill all fields and request it.
* [nRF SDK 12.3.0](https://developer.nordicsemi.com/nRF5_SDK/nRF5_SDK_v12.x.x/nRF5_SDK_12.3.0_d7731ad.zip).
  Download and unzip it anywhere (e.g. `C:/Dev/nRF5_SDK_12.3.0_d7731ad`), then in SES go to Tools -> Options -> Building -> Global macros
  and set NRF_SDK_12_PATH to path chosen above (e.g. `NRF_SDK_PATH=C:/Dev/nRF5_SDK_12.3.0_d7731ad`).
* Some additional files are required which aren't yet present in nRF SDK 12.3.0 (and more modern SDKs doesn't support nRF51 chips). To get
  them download [nRF SDK 15.3.0](https://developer.nordicsemi.com/nRF5_SDK/nRF5_SDK_v15.x.x/nRF5_SDK_15.3.0_59ac345.zip), unzip it
  somewhere and copy `modules` subfolder to the nRF SDK 12.3.0 folder.

To open the project in SES, open `ble_blinky_client_beacon.emProject` (this is a SES project file).

# Hardware setup
Requirements:
* One of [nRF devkits](https://www.nordicsemi.com/Software-and-Tools/Development-Kits).
* [nRF51 beacon](https://www.aliexpress.com/item/32953981724.html?spm=a2g0s.9042311.0.0.42b94c4d22qDa8).

Connect `VDD`, `GND`, `SWDIO` and `SWDCLK` according to the
[devkit](docs/devkit_programmer_pinout.png) and [beacon](docs/beacon_programmer_pinout.png) pinouts.

# Behaviour
On button press, for 1 seconds tries to discover advertising BLE devices fullfilling the following:
* Device name is `Nordic_Blinky`.
* RSSI is very high (device typically should be just a few centimetres away).
* Device exposes blinky service/characteristic.

If found, sends a characteristic write to the device and disconnects.

# Notes
Based on nRFs [BLE Blinky Client Application Example](https://infocenter.nordicsemi.com/topic/com.nordic.infocenter.sdk5.v15.3.0/ble_sdk_app_blinky_c.html?cp=5_1_4_2_0_0).
