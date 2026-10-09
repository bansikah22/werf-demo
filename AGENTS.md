# Project AI Instructions

## Context

This repository demonstrates a minimal Werf v3 delivery path: a Dockerfile-built static web image, a Helm chart, and GitHub Actions validation and deployment workflows. Read [README.md](README.md), [docs/project-context.md](docs/project-context.md), [docs/ci-cd.md](docs/ci-cd.md), and [docs/technology-currency.md](docs/technology-currency.md) before changing delivery configuration.

## Shared Engineering Skills

The canonical shared guidance source is [bansikah22/engineering-skills](https://github.com/bansikah22/engineering-skills). A local `../engineering-skills` checkout may be used for convenience, but is not required and must not be assumed after this project is cloned.

Before changing this repository, read the relevant shared guidance:

- CI actions, Werf, Helm, container images, or dependencies: [technology currency](https://github.com/bansikah22/engineering-skills/blob/master/workflows/technology-currency.md), [dependency changes](https://github.com/bansikah22/engineering-skills/blob/master/workflows/dependency-change.md), and [security](https://github.com/bansikah22/engineering-skills/blob/master/core/security.md).
- Delivery or application behavior: [new-feature workflow](https://github.com/bansikah22/engineering-skills/blob/master/workflows/new-feature.md) and [testing](https://github.com/bansikah22/engineering-skills/blob/master/core/testing.md).
- Meaningful delivery design alternatives: [technical decisions](https://github.com/bansikah22/engineering-skills/blob/master/decision-making/technical-decisions.md).

See [docs/engineering-skills-integration.md](docs/engineering-skills-integration.md) for how these references work across tools.

## Rules

- Use current official Werf, GitHub Actions, Kubernetes, Helm, and container-image documentation for version-sensitive changes.
- Pin external GitHub Actions and container base images to full immutable commit or manifest digests. Record the human-readable version and verification source in `docs/technology-currency.md`.
- Do not enable automatic production deployment. Keep deployment manually dispatched and protected by GitHub Environments.
- Do not commit kubeconfigs, registry credentials, tokens, or generated deployment secrets.
- Validate chart rendering and container builds after changes. Run a Werf build or converge when the required tool, registry, and cluster access are available.
