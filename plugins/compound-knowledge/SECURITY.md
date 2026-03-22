# Security

## Reporting Vulnerabilities

If you discover a security issue, please email austin@every.to.

## Design

This plugin is 100% markdown prompt files with no executable code, no dependencies, and no network access. The attack surface is limited to the prompt instructions themselves.

The plugin reads your project's `CLAUDE.md` for context. Ensure your `CLAUDE.md` does not contain secrets, as the plugin's review agents will process its contents.
