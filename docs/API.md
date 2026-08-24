# API Reference

> **Scope:** This repository contains the browser client, not the FastAPI backend implementation. This document records the compatible backend contract evidenced by the repository. Backend paths referenced by older development notes belong to a separate backend environment.

The compatible FastAPI service is documented as unauthenticated and intended for local-network use. The documented port is `8001`.

## Transport and controller bridge

- REST payloads use JSON.
- The backend bridge communicates with controllers over `/dev/serial0` at 1,000,000 baud with newline-delimited ASCII commands.
- Physical driver axes are `r`, `z`, `x1`, and `x2`; coordinated/virtual `x` and `p` are also used by motion helpers.
- Documented soft limits for coordinated motion: `x` 0..2100, `z` -11500..-50, `p` -255..255; `r` is unrestricted by the documented API helper.

## REST endpoints

### `GET /api/settings`
Returns current backend settings.

### `POST /api/settings`
Partial settings update. Unknown keys are documented as rejected.

### `POST /api/command`
Sends a raw controller-console command.

### `POST /api/moveabs`
Coordinated absolute move helper. Accepts any subset of integer `x`, `z`, `p`, and `r` targets, with at least one axis required.

### `POST /api/coordstatus`
Requests controller coordination status.

### `GET /api/coordstatus?refresh=1`
Returns the latest coordination-status line; `refresh=1` requests a fresh reading first.

### `POST /api/pos`
Requests current position.

### `GET /api/pos?refresh=1`
Returns the latest position line; `refresh=1` requests a fresh reading first.

### `POST /api/maxvelocity`
Query or set maximum velocity. Payload: `{ "axis": "<optional>", "sps": <optional integer 0-1000> }`.

### `POST /api/maxaccel`
Query or set maximum acceleration. Payload: `{ "axis": "<optional>", "sps2": <optional integer >=1> }`.

### `POST /api/measure`
Triggers VL6180X ranging. Payload: `{ "axis": "<label>", "seconds": <number> }`.

### `POST /api/led`
Updates axis LEDs using fields `axis`, `led0` through `led7`, and optional timing/brightness fields.

### `POST /api/stop`
Stops one axis when `{ "axis": "<label>" }` is supplied; an empty body performs a documented global stop.

### `POST /api/home`
Triggers Z-axis homing. The repository documentation states that the Z limit-switch condition is required.

### `POST /api/reboot`
Reboots a specific physical axis controller.

### `GET /api/driverstatus?axis=<axis>&refresh=1`
Returns driver status for a physical axis.

### `GET /api/driversettings?axis=<axis>&refresh=1`
Returns driver settings for a physical axis.

### `POST /api/driversettings`
Enables/disables a physical-axis driver.

## WebSockets

### `WS /ws/console`
Combined console/settings/metrics stream. The documented backend also accepts text controller commands through this socket.

### `WS /ws/axis/{axis_id}`
Per-axis stream for `r`, `z`, `x1`, or `x2`. The client uses `/ws/axis/r` for real-time range sampling.

Parsed metrics documented by the original API notes include `ts`, `ang`, `dps`, `dist`, `temp`, `lim`, `drv`, `cal`, `flt`, `rem`, `volt`, `amps`, `rpm`, `vel`, `spd`, `sps`, `range_mm`, and `range.err`.

## Generic examples

```bash
curl -X POST http://<host>:8001/api/moveabs \
  -H 'Content-Type: application/json' \
  -d '{"x":100,"z":-120,"p":0}'

curl 'http://<host>:8001/api/pos?refresh=1'

curl -X POST http://<host>:8001/api/measure \
  -H 'Content-Type: application/json' \
  -d '{"axis":"r","seconds":5}'

curl -X POST http://<host>:8001/api/stop \
  -H 'Content-Type: application/json' \
  -d '{}'
```

Use a hostname or address for **your** deployment; do not commit machine-specific endpoints to the repository.
