# Kinematics Setup

## 1. Choose standalone or hardware-connected use

The repository runs as a standalone 3D visualization. Live control is optional and uses the separate [ScanBot3000-control](https://github.com/DreamMakers2/ScanBot3000-control) FastAPI bridge.

## 2. Clone

```bash
git clone https://github.com/DreamMakers2/ScanBot3000-kinematics.git
cd ScanBot3000-kinematics
```

## 3. Review requirements

Read [REQUIREMENTS.md](REQUIREMENTS.md). Standalone visualization has substantially fewer requirements than the complete physical system.

## 4. Serve the web application

No build step or package installation is required for the checked-in frontend:

```bash
cd webapp
python -m http.server 8000
```

Open `http://localhost:8000/index.html`.

The page loads Three.js `0.157.0` from `unpkg.com` and fonts from Google Fonts, so those hosts must be reachable unless you vendor the assets yourself.

## 5. Standalone mode

With no API reachable, the application remains a visualization. Hardware-dependent controls report the backend as unavailable and cannot command live motion.

## 6. Full-stack mode

Set up the other project components first:

1. Flash/configure [ScanBot3000-firmware](https://github.com/DreamMakers2/ScanBot3000-firmware).
2. Configure and start [ScanBot3000-control](https://github.com/DreamMakers2/ScanBot3000-control) on the Raspberry Pi.
3. Confirm the control API can read `pos`/`coordstatus` from the firmware before connecting the kinematics UI.
4. Open the kinematics page with a runtime API override:

```text
http://localhost:8000/index.html?api=http://<host>:8001/api
```

Replace `<host>` with your control host locally. Do not commit that environment-specific value.

## 7. Validate before motion

1. Confirm API status becomes online.
2. Compare displayed positions with the physical machine.
3. Verify R/Z/X1/X2 naming and X/P coordinated behavior.
4. Verify Z homing and the physical limit switch.
5. Verify stop behavior with low-risk motion.
6. Run scan paths in dry-run mode first.
7. Confirm real physical clearance; the visualization is not a safety controller.

## 8. Local customization

Keep machine-specific endpoints, credentials, hostnames, local paths, and deployment data in runtime or ignored configuration. Do not commit them.

## 9. Troubleshooting

See [TROUBLESHOOTING.md](TROUBLESHOOTING.md) and the control/firmware troubleshooting guides for lower-layer issues.
