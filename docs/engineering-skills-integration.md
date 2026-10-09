# Engineering Skills Integration

## What Is Referenced

This project uses the shared guidance published at [bansikah22/engineering-skills](https://github.com/bansikah22/engineering-skills). [AGENTS.md](../AGENTS.md) is the local entry point: it tells an AI assistant which shared documents apply to the current task and points to this repository's local context and constraints.

For example, a change to a GitHub Actions workflow should use:

1. This project's `AGENTS.md`, `docs/ci-cd.md`, and `docs/technology-currency.md`.
2. The shared technology-currency, dependency-change, and security guidance.
3. Current official documentation for the action, Werf, GitHub Actions runner, or dependency being changed.

## Why It Uses Links Instead of a Submodule

The shared repository is referenced by canonical GitHub URLs rather than embedded as a Git submodule or copied into this project. This keeps project history focused and lets the shared guidance evolve independently. Project-specific instructions remain in this repository and take precedence when they intentionally differ.

## What Is Not Automatic

A Markdown reference does not install a skill into every AI tool or guarantee that an assistant can access the remote repository. An assistant must read `AGENTS.md` and retrieve the referenced guidance when its environment permits. When it cannot access the shared repository, it should say so rather than claiming the guidance was loaded.

For tools that support locally installed skills, install or copy the needed shared skill using that tool's documented mechanism. Keep the local project rules in `AGENTS.md`; do not duplicate the whole shared repository unless an offline workflow requires it.

## Update Model

- Improve generic engineering practices in `engineering-skills`.
- Improve Werf-specific constraints, credentials, namespaces, and commands in this repository.
- Update `docs/technology-currency.md` whenever an external action, runtime, base image, or delivery dependency changes.
