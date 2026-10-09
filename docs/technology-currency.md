# Technology Currency Record

Last verified: 2026-10-09

This file records the primary sources used for delivery-tool decisions. Recheck it when upgrading Werf, GitHub Actions, the base image, Kubernetes, or Helm.

| Component | Selected reference | Verification source | Notes |
| --- | --- | --- | --- |
| Werf | Stable v3 channel | [Official getting started](https://werf.io/getting_started/) | The project uses Werf v3 configuration and commands. |
| Werf setup action | `werf/trdl/actions/setup-app@2504624ea2798a206c277e8ebf250b495e3bab68` | [Official Werf GitHub Actions guide](https://werf.io/docs/v3/usage/integration_with_ci_cd_systems.html), resolved from tag `v0.13.0` | Pinned to the full commit SHA. |
| Checkout action | `actions/checkout@11d5960a326750d5838078e36cf38b85af677262` | [actions/checkout repository](https://github.com/actions/checkout), resolved from tag `v4` | Pinned to the full commit SHA. |
| Base image | `nginx:1.29-alpine@sha256:5616878291a2eed594aee8db4dade5878cf7edcb475e59193904b198d9b830de` | [Official Nginx Docker image](https://hub.docker.com/_/nginx), resolved with `docker buildx imagetools inspect` | Pinned to the multi-platform manifest digest. |
| Helm chart API | `v2` | [Helm chart format](https://helm.sh/docs/topics/charts/) | No chart dependencies are used. |

Do not replace an immutable reference with a floating tag. When updating a reference, review official release notes, compatibility implications, and the rendered chart and image build results.
