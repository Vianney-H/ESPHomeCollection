# ESPHome Lab

This workspace contains the ESPHome configuration for the ES3C28P board and a local CLI setup so you can validate, compile, and flash it without relying on the global ESPHome install.

## Available project commands

- `ESPHome: Validate Config`
- `ESPHome: Compile Firmware`

## Local CLI

The project uses the bundled local executable at `.venv\Scripts\esphome.exe`.

## Board documentation

This workspace targets an ESP32-S3 based touch display board of the ES3C28P family, with the following key capabilities:

- ESP32-S3 dual-core MCU
- 16 MB flash + Octal PSRAM
- 320x240 TFT display driven by ILI9341
- capacitive touch controller FT63x6
- ES8311 audio DAC + I2S microphone and speaker
- WS2812 status LED
- Wi‑Fi + Bluetooth proxy support
- Home Assistant-ready voice assistant integration

The configuration is intentionally self-contained and does not rely on a remote GitHub package for the base board definition. This keeps the project portable and easier to maintain.

See the full reference document: [docs/ES3C28P-reference.md](docs/ES3C28P-reference.md)

## Home Assistant entities currently exposed

The current configuration already exposes a set of useful entities in Home Assistant:

- `light.display_backlight_light` – backlight of the screen
- `light.status_led` – onboard RGB status LED
- `switch.enable_speaker_amp` – speaker amplifier enablement
- `button.redemarrer_ecran` – restart the device
- `binary_sensor.ecran_touche` – touch activity
- `binary_sensor.etat_esp32` – device online/status
- `sensor.signal_wifi` – Wi‑Fi signal quality
- `sensor.temps_dactivite` – uptime
- `sensor.temperature_esp32` – internal ESP32 temperature
- `text_sensor.adresse_ip` / `text_sensor.ssid_wifi` / `text_sensor.bssid_wifi` – Wi‑Fi details
- `media_player.haut_parleur` – speaker/media player for audio output

This is already a solid base for a wall-display / voice-assistant type device, and it covers the main board features without overloading the UI.

## Additional entities worth exposing

The board can support more Home Assistant objects depending on the desired usage:

- `camera` entities for each stream if you expose the refreshed web images as real camera entities
- `select` or `button` controls for switching the active camera stream manually
- `template switches` for screen auto-dim / refresh / display lock
- `event` or `text_sensor` for the active source name and current camera selection
- `number` entities for brightness or volume tuning if you want finer control over the UI and audio

For this project, the most useful additions are the temperature, status, and Wi‑Fi metadata entities already added so the ESP32 is easier to monitor from Home Assistant.

## Validate and compile

```powershell
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
