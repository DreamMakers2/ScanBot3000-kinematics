# Prompting Guide for AI/Agent Work

Use prompts that keep changes grounded in repository evidence and protect deployment-specific information.

## Code review

```text
Review this repository change for correctness and public-release safety. Do not invent hardware or backend behavior. Flag secrets, real private-network values, personal data, machine-specific paths, stale documentation, and behavior unsupported by the code or docs. Preserve existing functionality unless a security or correctness fix requires a change.
```

## Documentation update

```text
Update the documentation to match the current code. Separate verified facts from unknowns. Do not infer Raspberry Pi model, OS version, CPU architecture, RAM, storage, GPU, Teensy model, driver model, firmware version, or minimum hardware requirements unless the repository contains direct evidence.
```

## API integration

```text
Implement this client-side API change against docs/API.md. Keep the API endpoint runtime-configurable, use generic placeholders in examples, preserve offline visualization behavior, and do not commit machine-specific addresses or credentials.
```
