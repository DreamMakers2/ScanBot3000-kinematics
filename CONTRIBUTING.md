# Contributing

Contributions that improve correctness, portability, documentation, or the kinematics visualization are welcome.

## Development workflow

1. Branch from the current default branch.
2. Serve `webapp/` with a local HTTP server and verify standalone visualization.
3. If changing API integration, verify both offline behavior and a compatible local backend.
4. Keep changes focused and document only behavior supported by code, repository evidence, or a tested setup.
5. Run a privacy/security review before opening a pull request.

## Public-data rules

Do not commit secrets, tokens, credentials, real private-network addresses, machine names, MAC addresses, personal email addresses, identifying filesystem paths, private service names, GPS coordinates, or machine-specific configuration. Use `localhost`, `<host>`, documentation address ranges, and explicit placeholders in examples.

## Pull request checklist

- [ ] The browser client still loads and renders.
- [ ] API behavior is documented if changed.
- [ ] No generated files, caches, logs, local configuration, or editor state are included.
- [ ] No secrets or environment-specific identifiers are present in the diff.
- [ ] README, setup, requirements, API, security, and troubleshooting docs remain consistent.
- [ ] Licensing and third-party notices remain intact.
