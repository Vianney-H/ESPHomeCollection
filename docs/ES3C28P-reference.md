# ES3C28P reference

## Overview

The ES3C28P is an ESP32-S3 based development/display board designed for interactive touch interfaces. It combines a high-resolution TFT display, capacitive touch, audio I/O, and wireless connectivity in a compact module.

## Typical hardware features

- ESP32-S3 MCU
- 16 MB flash + octal PSRAM
- 320x240 TFT display driven by ILI9341
- capacitive touch controller FT63x6
- ES8311 audio DAC
- I2S microphone input
- I2S speaker output
- WS2812 RGB status LED
- Wi‑Fi and Bluetooth support
- Home Assistant-ready voice assistant integration

## ESPHome mapping used in this project

- `esp32`: `board: esp32-s3-devkitc-1`
- `display`: `platform: ili9xxx`, model `ILI9341`
- `touchscreen`: `platform: ft63x6`
- `microphone`: I2S external ADC input
- `speaker`: I2S external DAC output via ES8311
- `light`: screen backlight and status LED
- `lvgl`: landscape orientation enabled with `rotation: 90`
- `web_server`: local web interface
- `bluetooth_proxy`: Bluetooth passthrough
- `voice_assistant`: local assistant / speech interface

## Why this design is useful

This kind of board is ideal for a Home Assistant wall panel or smart display because it can combine:

- local UI rendering with LVGL
- camera snapshots or external HTTP images
- ambient display / smart dashboard interaction
- voice input and audio output
- network diagnostics and BT proxy capabilities

## Home Assistant relevance

The board is already well suited for HA because it can expose multiple classes of entities:

- lights
- switches
- buttons
- sensors
- text sensors
- media player
- binary sensors
- voice assistant integration

## Good next improvements

For a production display, the most valuable additional entities are:

1. Wi‑Fi and IP metadata
2. internal ESP32 temperature
3. online/offline status
4. manual camera-source switching buttons
5. display brightness controls
6. dedicated audio controls or source selection

This keeps the board useful in Home Assistant without adding unnecessary complexity.