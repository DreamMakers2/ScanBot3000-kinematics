# Kinematics Requirements

This document distinguishes the standalone browser client from the optional full ScanBot3000 hardware stack. It does not invent numeric minimums that are not supported by repository evidence.

## Standalone visualization

### Verified software requirements

- A browser capable of running the static HTML/CSS/JavaScript in `webapp/`.
- WebGL support sufficient for `THREE.WebGLRenderer` in Three.js `0.157.0`.
- Network access to `unpkg.com` for Three.js and Google Fonts for the configured fonts, unless those resources are vendored locally.
- A static HTTP server is recommended. The documented example uses `python -m http.server 8000`; no Python version is pinned by this repository.

There is no Node.js/npm build, package manifest, frontend lockfile, or bundler requirement in the checked-in project.

### CPU, RAM, storage, GPU

No numeric CPU, RAM, storage, or GPU minimum has been measured or recorded for the browser client. A WebGL-capable browser is the only defensible functional graphics requirement. A discrete GPU is not documented as required.

## Full hardware-connected project

When live control is enabled, the linked repositories establish the following project configuration.

### Control host

From `ScanBot3000-control`:

- Raspberry Pi 4B.
- 2 GB RAM in the recorded deployment.
- Linux/systemd-style environment.
- Python 3.10+ in the existing setup requirements.
- FastAPI/Uvicorn/pyserial stack.
- `/dev/serial0` at 1,000,000 baud to the Teensy.

No lower Raspberry Pi model, RAM minimum, storage minimum, or exact OS release is claimed.

### Embedded controllers

From `ScanBot3000-firmware`:

- Teensy 4.1 motion supervisor.
- ESP32-S3 DevKitC-1 class axis-controller target.
- TMC2209 stepper drivers.
- Physical axes R, Z, X1, X2 and virtual X/P behavior.
- DS18B20 temperature sensing, limit switches, SSD1306 OLED, WS2812B/NeoPixel indicators.
- AS5600 encoders on non-R axes.
- VL6180X time-of-flight sensor on the R axis.

Exact motor models, power-supply sizing, mechanics, travel clearances, and generalized hardware minimums are not established by this repository set and must not be inferred from the visualization.

## Networking

Live control requires a network path from the browser to `ScanBot3000-control`. The API is unauthenticated and is intended for a trusted local network. No particular Ethernet/Wi-Fi hardware is mandated by code.

## API/serial constraints

- HTTP API base is runtime-configurable; examples use `http://<host>:8001/api`.
- Axis WebSocket paths use `/ws/axis/{axis_id}`.
- The control bridge talks to the Teensy over `/dev/serial0` at 1,000,000 baud in the verified project configuration.
- Z homing and firmware motion limits remain authoritative; the 3D client is not a safety envelope.
