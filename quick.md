
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