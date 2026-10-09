# CI/CD Configuration

## Verification

The [verify workflow](../.github/workflows/verify.yml) runs on pull requests and `main` pushes using the pinned `ubuntu-24.04` runner. It performs these checks:

1. Checks out the full Git history required by Werf.
2. Installs the stable Werf v3 toolchain through its official setup action.
3. Renders the Helm chart using Werf's Helm wrapper.
4. Runs `werf build --dev`, which builds the image without publishing it to a registry.

## Deployment

The [deploy workflow](../.github/workflows/deploy.yml) runs only through `workflow_dispatch`. It uses the selected GitHub Environment, initializes Werf's GitHub CI environment with `werf ci-env github`, and runs `werf converge`.

Before enabling a deployment environment:

1. Create the GitHub Environment, such as `development` or `staging`.
2. Add `KUBE_CONFIG_BASE64`, containing a base64-encoded kubeconfig for that environment.
3. Configure environment protection rules for deployment approval where appropriate.
4. Ensure the Kubernetes identity can modify only the required namespace and resources.
5. Verify GitHub Actions has `packages: write` permission for GHCR publishing.

The workflow does not deploy automatically on a push. This is intentional for a learning project and avoids deploying to an unconfigured cluster.
