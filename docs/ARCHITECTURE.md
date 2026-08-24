# Architecture

The repository contains a static Three.js browser client. Optional live control connects to a separately maintained FastAPI service, which bridges local-network requests to machine controllers over UART.

```mermaid
flowchart LR
    U[Operator browser] -->|Static HTML/CSS/JS| W[Three.js client<br/>webapp/]
    W -->|REST /api/*| A[Compatible FastAPI bridge<br/>separate deployment]
    W -->|WebSocket /ws/axis/r| A
    A -->|/dev/serial0<br/>1,000,000 baud ASCII| T[Teensy axis controllers]
    T --> X[Physical axes<br/>r · z · x1 · x2]
    T --> D[TMC driver interface<br/>model not recorded]
    T --> L[Z limit switch]
    T --> R[VL6180X range sensor<br/>R axis]
```

## Browser client

`webapp/index.html`, `styles.css`, and `app.js` implement the visualization and operator controls. Three.js `0.157.0` is loaded at runtime from unpkg. The client can remain in visualization mode when the backend is unavailable.

## API bridge

The backend source is not part of this repository. `API.md` records the compatible contract used by the client: motion, positions, homing, driver state/settings, LEDs, ranging, reboot, stop, and WebSocket telemetry.

## Controller side

Repository evidence identifies Teensy controllers, physical axes `r`, `z`, `x1`, `x2`, TMC driver commands, a Z limit switch, and VL6180X ranging. Exact board, driver, motor, power, mechanics, and firmware versions are not recorded here.

## Trust boundary

The documented compatible API is unauthenticated and intended for a trusted local network. It should not be exposed directly to the public internet.
