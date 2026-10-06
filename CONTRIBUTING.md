# Contributing

These guidelines apply to every repository in this organization unless a repository ships its own `CONTRIBUTING`.

## Issues

Use the issue templates. For a bug, include the version, reproduction steps, and expected versus actual behavior.
For a security problem, follow [SECURITY.md](SECURITY.md) instead.

## Pull requests

1. Fork, then branch from the default branch.
2. Keep each pull request to one concern.
3. Use a [Conventional Commit](https://www.conventionalcommits.org/) subject as the PR title, for example
   `feat(zip): add streaming extraction`. Releases derive the version from it.
4. Add tests for new behavior and confirm the status checks pass.

Library-specific rules (code style, build, API compatibility checks) live in the
[compress4j CONTRIBUTING guide](https://github.com/hominux/compress4j/blob/main/.github/CONTRIBUTING.adoc).

Contributions are accepted under the license the repository declares.
