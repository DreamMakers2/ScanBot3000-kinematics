# Requirements

This document separates repository-evidenced configuration from unknowns. It intentionally does not invent minimum specifications.

## Verified project configuration

### Browser / visualization side

- A browser capable of running the static HTML/CSS/JavaScript application in `webapp/`.
- WebGL support sufficient for `THREE.WebGLRenderer` in Three.js `0.157.0`.
- Network access to `unpkg.com` for Three.js and Google Fonts for the configured fonts, unless those assets are vendored locally.
- No frontend build system, package manager, lockfile, or package manifest is present.

### Machine-control side

Repository evidence shows integration with:

- A **Raspberry Pi** hosting a compatible FastAPI bridge. The exact Pi model, RAM, storage, CPU generation, and 32/64-bit architecture are not recorded.
- A Linux-style serial device at `/dev/serial0` at **1,000,000 baud**, using newline-delimited ASCII controller commands.
- **Teensy-based axis controllers**. The exact Teensy model and firmware version are not recorded.
- Physical axis identifiers `r`, `z`, `x1`, and `x2`, plus coordinated/virtual `x` and `p` behavior in the API.
- Driver/TMC status and settings commands. The exact Trinamic/TMC part number, motor type, current, voltage, gearing, and mechanics are not recorded.
- A **Z-axis limit switch** used by the documented homing command.
- A **VL6180X** time-of-flight ranging sensor associated with the R axis for point-cloud sampling.
- Local-network HTTP and WebSocket connectivity between the browser and the compatible API, using port `8001` in the documented setup.

## Minimum requirements

No defensible numeric CPU, RAM, storage, GPU, Raspberry Pi model, motor-driver model, or power-supply minimum can be derived from this repository, so those values are **not specified**.

Evidence-supported functional minimums are:

- A WebGL-capable browser for visualization.
- Enough resources to serve and run a small static web application; no numeric threshold is documented.
- For hardware control, a compatible API implementation exposing the documented REST/WebSocket contract and communicating with the project controllers.
- A network path from the browser to that API.

## Recommended requirements

The repository contains no benchmarks or qualification data sufficient to recommend specific CPU, RAM, storage, GPU, Raspberry Pi, driver, motor, or power specifications. Use hardware you have validated for your machine and document it separately.

A discrete GPU is **not documented as required**. Hardware-accelerated WebGL is appropriate for smoother rendering, but no GPU model or performance class is verified here.

## Software requirements

### Frontend

- Static HTML/CSS/JavaScript.
- Three.js `0.157.0`, loaded from `unpkg.com` by `webapp/index.html`.
- IBM Plex Mono and Space Grotesk, loaded through Google Fonts.
- No npm, Node.js, bundler, or frontend dependency manifest is required by the checked-in project.
- A local static server is recommended. The documented example uses `python -m http.server 8000`; no Python version is pinned.

### Compatible backend

- The separate backend is described as a **FastAPI** service.
- The exact Python version, FastAPI version, ASGI server, dependency lockfile, OS release, and package-manager versions are **not present in this repository**.
- `/dev/serial0` and a documented `iptables` port-forward helper indicate a Linux/Raspberry Pi-style deployment, but the exact distribution and kernel are not recorded.
- Backend source, dependency installation, controller firmware, and firmware flashing procedures are not included.

## Interfaces and constraints

- HTTP API base: configurable; examples use `http://<host>:8001/api`.
- WebSocket path: `/ws/axis/{axis_id}` on the same host.
- UART: `/dev/serial0`, 1,000,000 baud, newline-delimited ASCII according to the API reference.
- Z homing depends on the documented limit-switch condition.
- Motion limits and controller semantics are documented in `API.md`; do not infer safe physical travel or clearances from the visualization alone.
