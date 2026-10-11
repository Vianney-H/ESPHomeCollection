# ESPHome Lab

This workspace contains the ESPHome configuration for the ES3C28P board and a local CLI setup so you can validate, compile, and flash it without relying on the global ESPHome install.

## Available project commands

- `ESPHome: Validate Config`
- `ESPHome: Compile Firmware`

## Local CLI

The project uses the bundled local executable at `.venv\Scripts\esphome.exe`.

## Validate and compile

```powershell
cd C:\Users\viann\projects\esphome-lab
.\.venv\Scripts\esphome.exe config .\ES3C28P.yaml
.\.venv\Scripts\esphome.exe compile .\ES3C28P.yaml
```

## Flash to the device

After a successful build, you can upload the firmware to the ESP32 over USB.

### Standard USB serial flash

```powershell
cd C:\Users\viann\projects\esphome-lab
.\.venv\Scripts\esphome.exe run .\ES3C28P.yaml --device COM6
```

If your board is on a different COM port, replace `COM6` with the correct one from Device Manager.

### OTA flash over Wi‑Fi

```powershell
cd C:\Users\viann\projects\esphome-lab
.\.venv\Scripts\esphome.exe run .\ES3C28P.yaml --device 192.168.1.108
```

This works once the ESP32 has already been flashed and connected to the same Wi‑Fi network.

### Upload only

```powershell
cd C:\Users\viann\projects\esphome-lab
.\.venv\Scripts\esphome.exe upload .\ES3C28P.yaml --device COM6
```

## Useful reminder

> The config expects `wifi_ssid`, `wifi_password`, and `api_encryption_key` to be defined in `secrets.yaml`.

> For serial flashing, the device must be connected to the computer and visible in the system as a COM port.
