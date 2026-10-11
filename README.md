# ESPHome Lab

This workspace contains a minimal ESPHome config and a custom VS Code task to validate and compile it with the bundled local CLI.

## Commands

- `ESPHome: Validate Config`
- `ESPHome: Compile Firmware`

## Local CLI

The project uses the venv-installed ESPHome executable at `.venv\Scripts\esphome.exe`.

## Example

```powershell
.\.venv\Scripts\esphome.exe config .\ES3C28P.yaml
.\.venv\Scripts\esphome.exe compile .\ES3C28P.yaml
```

> The config expects `wifi_ssid` and `wifi_password` secrets to be defined in `secrets.yaml`.
