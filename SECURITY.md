# Security Policy

## Security model

The web client is a static application. Its optional machine-control features connect to a separate FastAPI service over HTTP and WebSocket. The API contract in this repository describes that service as **unauthenticated** and intended for a trusted local network. Do not expose a compatible control API directly to the public internet.

The client can send motion, driver, homing, LED, ranging, reboot, and emergency-stop commands. Treat the API host as equipment-control infrastructure, not as a public web service.

## Deployment guidance

- Keep the control API on a trusted/private network or behind an access-control layer you operate.
- Restrict CORS and network reachability to the clients that need access.
- Keep machine-specific endpoints out of source control; use runtime configuration.
- Do not place credentials in query strings or repository files.
- Validate homing, limits, emergency-stop behavior, and physical clearances on the actual machine before enabling motion.

## Reporting a vulnerability

Use a private GitHub Security Advisory for this repository when that feature is available. Do not post credentials, private infrastructure details, or an unpatched exploit in a public issue.

No response-time commitment is stated by this project.
