
```
python -m venv .venv
source .venv/bin/activate
# Or
.\.venv\Scripts\Activate.ps1
```

```
pip install platformio dronecan setuptools empy==3.3.4 pexpect
```


```
cd src
pio run --environment Unified_ESP32_900_RX_via_BetaflightPassthrough
pio run --environment Unified_ESP32_2400_TX_via_UART
```

* Flashing:

```
pio run --target upload --environment Unified_ESP32_2400_TX_via_UART --upload-port /dev/ttyUSB0

pio run --target upload --environment Unified_ESP32_2400_TX_via_UART --upload-port COM15
```


* See log:

```
pio device monitor --port COM15 --baud 115200
# On windows just use putty to see the log, set baudrate to 115200
```

