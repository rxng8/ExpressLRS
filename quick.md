
```
python -m venv .venv
source .venv/bin/activate
# Or
.\.venv\Scripts\Activate.ps1
```

```bash
conda create -n elrs python=3.10
conda activate elrs
```

```bash
pip install platformio dronecan setuptools empy==3.3.4 pexpect
```

* Testing
```
cd src
pio run --environment Unified_ESP32_900_RX_via_BetaflightPassthrough
pio run --environment Unified_ESP32_2400_TX_via_UART
```

```bash
pio run --environment Unified_ESP32S3_2400_TX_via_UART
pio run --environment Unified_ESP32S3_2400_RX_via_UART
```


* Build and Flashing:

```
pio run --target upload --environment Unified_ESP32_2400_TX_via_UART --upload-port /dev/ttyUSB0

pio run --target upload --environment Unified_ESP32_2400_TX_via_UART --upload-port COM15
```

```bash
# Build TX
pio run --target upload --environment Unified_ESP32S3_2400_TX_via_UART --upload-port /dev/ttyACM0
# option 2

# Build RX
pio run --target upload --environment Unified_ESP32S3_2400_RX_via_UART --upload-port /dev/ttyACM0
# option 1
```



* See log:

```
pio device monitor --port COM15 --baud 115200
# On windows just use putty to see the log, set baudrate to 115200
```

baud: 115200 for boot
baud: 460800 for normal logging

```bash
screen /dev/ttyACM0 115200

ls -l /dev/serial/by-id/
pio device monitor --port /dev/serial/by-id/usb-FTDI_FT232R_USB_UART_BH00OO57-if00-port0 --baud 460800
```


add

```
-D DEBUG_LOG
```

to

```ini
[env_common_esp32tx]
extends = env_common_esp32
monitor_speed = 460800
lib_deps =
	${env_common_esp32.lib_deps}
	h2zero/NimBLE-Arduino @ 2.3.6
	lemmingdev/ESP32-BLE-Gamepad @ 0.7.4
	olikraus/U8g2 @ 2.36.12
	moononournation/GFX Library for Arduino @ 1.6.0
build_src_filter = ${common_env_data.build_src_filter} -<rx_*.cpp> -<rx-*/>
build_flags =
	${env_common_esp32.build_flags}
	${common_env_data.build_flags_tx}
	-include target/Unified_ESP32_TX.h
	-D VTABLES_IN_FLASH=1
  -D DEBUG_LOG
	-D DEBUG_TX_FREERUN
	-D DEBUG_TX_SYNTHETIC_RC
	-O2
```

to [esp32-tx.ini](./src/targets/esp32-tx.ini)


to enable debugging


* Bind: they use a phrase defined in user-defines.txt or `-DMY_BINDING_PHRASE="your-unique-test-phrase"`


