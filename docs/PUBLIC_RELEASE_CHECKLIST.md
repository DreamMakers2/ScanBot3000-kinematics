# Public Release Checklist

## Repository state

- [x] Canonical repository name and title use `ScanBot3000-kinematics` / `ScanBot3000 Kinematics`.
- [x] README links the project home, canonical control server, and firmware repositories.
- [x] Setup/requirements/architecture docs now use the actual linked project components instead of treating their known hardware as unknown.
- [x] Apache License 2.0 + Commons Clause 1.0, NOTICE, CONTRIBUTING, SECURITY, setup, requirements, API, architecture, troubleshooting, and prompting docs are present.

## Privacy/security

- [x] `.gitignore` excludes local endpoint configuration, `.env` files, build output, caches, logs, and editor state.
- [x] Current-tree review contains placeholders such as `<host>` instead of real deployment endpoints.
- [x] No credentials, API keys, passwords, personal email addresses, real private-network addresses, MAC addresses, identifying filesystem paths, or private hostnames are retained in project files.
- [x] Security docs state that the downstream motion-control API is unauthenticated and intended for a trusted LAN.

## History

- [x] Previous development/public-cleanup history was reviewed before final release normalization.
- [x] `main` is rewritten to one parentless `Initial public release` commit containing the sanitized current tree.
- [x] No additional repository branches were present during the audit.
- [x] No tag namespace was returned by the available Git-ref check during the audit.

## Accuracy

- [x] Three.js version and static frontend structure match repository source.
- [x] Full-stack hardware details are now grounded in the linked firmware/control repositories.
- [x] Unknown browser CPU/RAM/storage/GPU minimums remain explicitly unknown.
- [x] API endpoint examples use placeholders rather than deployment-specific values.

## Final operator review

Before further publication/announcement, review the rendered architecture SVG, API endpoint configuration, and physical-motion warnings against the current machine.
