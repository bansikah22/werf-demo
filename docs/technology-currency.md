# Technology Currency Record

Last verified: 2026-10-09

This file records the primary sources used for delivery-tool decisions. Recheck it when upgrading Werf, GitHub Actions, the base image, Kubernetes, or Helm.

| Component | Selected reference | Verification source | Notes |
| --- | --- | --- | --- |
| Werf | Stable group `2`, channel `stable` (currently v2.79.2) | [Official getting started](https://werf.io/getting_started/) and verified with `trdl update werf 2 stable` | The v3 CI example's `stable` channel does not currently resolve; use the verified stable channel. |
| Werf setup action | `werf/trdl/actions/setup-app@2504624ea2798a206c277e8ebf250b495e3bab68` | [Official Werf GitHub Actions guide](https://werf.io/docs/v3/usage/integration_with_ci_cd_systems.html), resolved from latest tag `v0.13.0` | Pinned to the full commit SHA. |
| Checkout action | `actions/checkout@3d3c42e5aac5ba805825da76410c181273ba90b1` | [actions/checkout repository](https://github.com/actions/checkout), resolved from tag `v7` | v7 avoids the deprecated Node 20 runtime and is pinned to the full commit SHA. |
| GitHub Actions runner | `ubuntu-24.04` | [GitHub-hosted runners](https://docs.github.com/actions/concepts/runners/github-hosted-runners) | Pinned to avoid an unreviewed `ubuntu-latest` migration. |
| Base image | `nginx:1.29-alpine@sha256:5616878291a2eed594aee8db4dade5878cf7edcb475e59193904b198d9b830de` | [Official Nginx Docker image](https://hub.docker.com/_/nginx), resolved with `docker buildx imagetools inspect` | Pinned to the multi-platform manifest digest. |
| Helm chart API | `v2` | [Helm chart format](https://helm.sh/docs/topics/charts/) | No chart dependencies are used. |

Do not replace an immutable reference with a floating tag. When updating a reference, review official release notes, compatibility implications, and the rendered chart and image build results.
