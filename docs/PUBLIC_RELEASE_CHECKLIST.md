# Public Release Checklist

## Current-tree privacy and security

- [ ] Remove the real private-network API endpoint from `webapp/app.js` and replace it with a generic/runtime-configurable value.
- [ ] Remove the project-specific organization/copyright label from `webapp/index.html`.
- [x] Add public contribution and security guidance.
- [x] Add evidence-based setup, requirements, architecture, troubleshooting, and prompting documentation.
- [ ] Run a final current-tree scan for exact IPs, emails, MAC addresses, identifying home-directory paths, hostnames/private domains, GPS/location data, credentials, internal names, and stale references.

## Git history

- [x] Enumerated reachable commits and normal branches before cleanup.
- [x] Identified a real LAN endpoint and identifying commit/history metadata requiring removal.
- [ ] Rewrite retained Git history so sensitive values are removed from historical blobs and commit metadata, not merely deleted in a newer commit.
- [ ] Verify all retained branches and tags after the rewrite no longer reach sensitive history.

## Repository surface

- [x] README/public documentation work is staged on `public-ready-review`.
- [x] `CONTRIBUTING.md` and `SECURITY.md` are present.
- [x] Hardware/software requirements distinguish verified facts from unknowns.
- [ ] Finalize `LICENSE` and `NOTICE` with Apache License 2.0 plus Commons Clause 1.0 terms.
- [ ] Finalize the architecture infographic and README links.
- [ ] Remove one-shot sanitization tooling from the final public tree after history cleanup succeeds.

## Release gate

Do **not** treat this branch as public-ready until every unchecked privacy/history item above is complete and re-verified. Repository visibility must not be changed as part of this checklist.
