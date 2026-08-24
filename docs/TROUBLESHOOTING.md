# Troubleshooting

These entries are grounded in current client behavior and the checked-in API contract. They do not assert an unverified compatibility matrix.

## The page renders but API status stays offline

- Confirm the separate FastAPI service is running.
- Confirm the configured API URL ends in `/api`, for example `http://<host>:8001/api`.
- Check network reachability and the backend CORS policy.
- Standalone visualization is expected to continue working while the API is offline.

## Point-cloud sampling reports a WebSocket problem

The client opens `/ws/axis/r` on the API host. Confirm the compatible backend implements that path and that any proxy/firewall permits WebSocket upgrades.

## Three.js or fonts do not load

`webapp/index.html` loads Three.js `0.157.0` from `unpkg.com` and fonts from Google Fonts. Blocked or offline CDN access can prevent normal rendering or change typography. Vendor those assets for offline deployments.

## WebGL initialization fails

The client reports `WebGL init failed` if `THREE.WebGLRenderer` cannot initialize. Use a browser/device with functioning WebGL support and graphics drivers. No specific GPU/browser version matrix is documented here.

## Motion controls are disabled

Direct control is gated on API health and the homed state. Verify the backend reports the expected status and complete the required homing sequence.

## Driver status/settings fail

The API reference restricts driver/TMC operations to physical axes (`r`, `z`, `x1`, `x2`) or labels resolving to them. Virtual `x`/`p` are not valid for those endpoints.

## Z homing fails

The documented backend command depends on the Z limit-switch condition. Verify the actual switch, wiring, controller firmware, and backend console behavior for your hardware.
