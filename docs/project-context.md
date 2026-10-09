# Project Context: Werf Demo

## Purpose

Provide a small, inspectable repository for learning how Werf v3 connects a Dockerfile image build, Helm chart, and GitHub Actions CI/CD flow.

## Scope and Non-Goals

The service is a static Nginx page. It demonstrates delivery mechanics, not application development, ingress configuration, persistent data, multi-service architecture, or production observability.

## Constraints

- The project must remain small enough to understand in one sitting.
- CI uses immutable references for external actions.
- Deployment is manual and requires an explicitly configured GitHub Environment and Kubernetes credentials.
- The repository may be public, so it contains no credentials or cluster-specific values.

## Architecture Summary

`werf.yaml` declares one image, `web`, built from the root Dockerfile. The `.helm` chart deploys that image as a Kubernetes Deployment and exposes it with a ClusterIP Service. The image reference is supplied through Werf's `global.werf.images.web.ref_tag` value during convergence.

## Development

Use the commands in [README.md](../README.md) for Helm, Docker, and Werf validation.

## Operations

The deployment workflow requires a base64-encoded kubeconfig stored in the target GitHub Environment as `KUBE_CONFIG_BASE64`. The workflow publishes images through GHCR and deploys using `werf converge`.
