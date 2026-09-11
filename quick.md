
```
python -m venv .venv
source .venv/bin/activate
# Or
.\.venv\Scripts\Activate.ps1
```

```
pip install platformio dronecan setuptools empy==3.3.4 pexpect
```

* Testing
```
cd src
pio run --environment Unified_ESP32_900_RX_via_BetaflightPassthrough
pio run --environment Unified_ESP32_2400_TX_via_UART
```

* Build and Flashing:

```
pio run --target upload --environment Unified_ESP32_2400_TX_via_UART --upload-port /dev/ttyUSB0

pio run --target upload --environment Unified_ESP32_2400_TX_via_UART --upload-port COM15
```


* See log:

```
pio device monitor --port COM15 --baud 115200
# On windows just use putty to see the log, set baudrate to 115200
```

baud: 115200 for boot
baud: 460800 for normal logging


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
	-O2
```

to [esp32-tx.ini](./src/targets/esp32-tx.ini)


to enable debugging
