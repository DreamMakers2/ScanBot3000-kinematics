# Setup

## 1. Choose standalone or hardware-connected use

The repository can run as a standalone 3D visualization. Hardware control is optional and requires a **separate compatible FastAPI backend** implementing the contract in [API.md](API.md).

## 2. Get the repository

```bash
git clone <your-repository-url>
cd Scanbot3000_Kinematics
```

If you rename the repository, use the new directory name.

## 3. Review requirements

Read [REQUIREMENTS.md](REQUIREMENTS.md). The exact Raspberry Pi model, OS version, Teensy model, motor-driver model, and power hardware are not recorded in this repository.

## 4. Serve the web application

No build step is required:

```bash
cd webapp
python -m http.server 8000
```

Open `http://localhost:8000/index.html`.

The page loads Three.js `0.157.0` from `unpkg.com` and fonts from Google Fonts, so those hosts must be reachable unless you vendor the assets yourself.

## 5. Standalone mode

With no compatible API reachable, the application remains a visualization. API-driven controls report the backend as offline and cannot command live motion.

## 6. Connect your own compatible API

Start your separately maintained backend and verify it implements [API.md](API.md). Public-ready configuration should use loopback by default and allow a runtime override, for example:

```text
http://localhost:8000/index.html?api=http://<host>:8001/api
```

Replace `<host>` with your backend hostname or address. Do not commit that environment-specific value.

## 7. Validate before enabling machine motion

1. Confirm the API status becomes online.
2. Verify position readouts against the physical machine.
3. Verify axis naming and configured limits.
4. Verify Z homing and the physical limit switch.
5. Verify emergency-stop behavior.
6. Use dry-run scan mode before commanding a physical scan path.
7. Confirm physical clearances and safe travel; the visualization is not a safety controller.

## 8. Local customization

Keep machine-specific endpoints, credentials, hostnames, and local paths in runtime or untracked configuration. Do not commit them.

## 9. Troubleshooting

See [TROUBLESHOOTING.md](TROUBLESHOOTING.md).
