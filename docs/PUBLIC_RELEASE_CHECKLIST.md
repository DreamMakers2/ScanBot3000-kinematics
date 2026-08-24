# Public Release Checklist

## Current-tree privacy and security

- [x] Replace the real private-network API endpoint in `webapp/app.js` with a localhost default and runtime `?api=` override.
- [x] Remove the project-specific organization/copyright label from `webapp/index.html`.
- [x] Add public contribution and security guidance.
- [x] Add evidence-based setup, requirements, architecture, troubleshooting, and prompting documentation.
- [x] Run a final current-tree scan for known exact private identifiers and review the retained public tree for machine-specific configuration, credentials, internal notes, and stale private references.

## Git history

- [x] Enumerated reachable commits and normal branches before cleanup.
- [x] Identified a real LAN endpoint and identifying commit/history metadata requiring removal.
- [ ] Rewrite retained Git history so sensitive values are removed from historical blobs and commit metadata, not merely deleted in a newer commit.
- [ ] Verify all retained branches and tags after the rewrite no longer reach sensitive history.

## Repository surface

- [x] README/public documentation work is staged on `public-ready-review`.
- [x] `CONTRIBUTING.md` and `SECURITY.md` are present.
- [x] Hardware/software requirements distinguish verified facts from unknowns.
- [x] `LICENSE` and `NOTICE` contain Apache License 2.0 plus Commons Clause 1.0 terms and notices.
- [x] Architecture infographic, Mermaid diagram, and README documentation links are present.
- [x] The one-shot destructive sanitization workflow is absent from the review tree.
- [x] Internal agent notes and the duplicate backend-context path are absent from the review tree.

## Release gate

The **current tree** on `public-ready-review` has been prepared for review, but the repository is **not history-clean yet**. Do not treat the repository as fully public-ready until both unchecked Git-history items above are completed and re-verified. Repository visibility must not be changed as part of this checklist.
