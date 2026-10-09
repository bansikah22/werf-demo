# Project AI Instructions

## Context

This repository demonstrates a minimal Werf v3 delivery path: a Dockerfile-built static web image, a Helm chart, and GitHub Actions validation and deployment workflows. Read [README.md](README.md), [docs/project-context.md](docs/project-context.md), [docs/ci-cd.md](docs/ci-cd.md), and [docs/technology-currency.md](docs/technology-currency.md) before changing delivery configuration.

## Shared Engineering Skills

Use the sibling `engineering-skills` repository as the shared guidance source. The most relevant documents are the technology-currency workflow, dependency-change workflow, security guidance, and new-feature workflow.

## Rules

- Use current official Werf, GitHub Actions, Kubernetes, Helm, and container-image documentation for version-sensitive changes.
- Pin external GitHub Actions and container base images to full immutable commit or manifest digests. Record the human-readable version and verification source in `docs/technology-currency.md`.
- Do not enable automatic production deployment. Keep deployment manually dispatched and protected by GitHub Environments.
- Do not commit kubeconfigs, registry credentials, tokens, or generated deployment secrets.
- Validate chart rendering and container builds after changes. Run a Werf build or converge when the required tool, registry, and cluster access are available.
