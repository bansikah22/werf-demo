# Homelab Deployment Guide

This guide deploys the current checkout directly to the Kubernetes cluster selected by your local `kubectl` context. It does not use GitHub Actions or require a cluster kubeconfig to leave your homelab.

## Prerequisites

- Docker is running on the machine that runs Werf.
- `kubectl` is configured for the intended cluster.
- Werf v2 is installed.
- The cluster nodes can pull from a container registry reachable from the homelab.
- You can push to that registry from the deployment machine.

For a first deployment, use a registry that the cluster can pull without credentials. This chart does not yet configure Kubernetes `imagePullSecrets`; private-registry support should be added before using a private registry.

## Deploy

Run these commands from the root of this repository. Replace the registry hostname with your homelab registry.

```sh
# Stop if kubectl is pointing at an unexpected cluster.
kubectl config current-context
kubectl cluster-info

# Authenticate to the registry that both this machine and cluster nodes can reach.
docker login registry.home.arpa:5000

# Choose the deployment identity. These names are used consistently below.
export WERF_ENV=development
export WERF_REPO=registry.home.arpa:5000/werf-demo
export WERF_NAMESPACE=werf-demo-development
export WERF_RELEASE=werf-demo-development

# Optional: expose this local demonstration through the cluster's ingress.
export WERF_INGRESS_HOST=werf-demo.localhost

# Create the isolated namespace if it does not exist.
kubectl create namespace "$WERF_NAMESPACE" --dry-run=client -o yaml | kubectl apply -f -

# Build the image, push it to the registry, apply the Helm chart, and wait for readiness.
werf converge \
  --env "$WERF_ENV" \
  --repo "$WERF_REPO" \
  --namespace "$WERF_NAMESPACE" \
  --release "$WERF_RELEASE" \
  --set ingress.enabled=true \
  --set ingress.className=traefik \
  --set ingress.host="$WERF_INGRESS_HOST" \
  --atomic
```

`--atomic` rolls the release back if it cannot become ready. Do not use `--dev` for this shared-cluster deployment: it is intended for local uncommitted development.

## Verify And Access

The chart's names are derived from the chosen release and chart name. With the variables above, the Deployment and Service are named `werf-demo-development-werf-demo`.

```sh
kubectl -n "$WERF_NAMESPACE" get deployment,service,pods
kubectl -n "$WERF_NAMESPACE" rollout status deployment/werf-demo-development-werf-demo
kubectl -n "$WERF_NAMESPACE" port-forward service/werf-demo-development-werf-demo 8080:80
```

Open `http://localhost:8080` while the port-forward is running. The expected page title is `Werf Demo`.

When the optional ingress settings above are enabled on the local K3d cluster,
open `http://werf-demo.localhost:58088` instead. Ingress is disabled by default
so other environments can choose their own controller and host name.

## Update Or Remove

Run the same `werf converge` command after changing the application or chart. Werf builds and publishes a content-addressed image, then updates the Helm release.

To remove the demo:

```sh
werf dismiss \
  --env "$WERF_ENV" \
  --namespace "$WERF_NAMESPACE" \
  --release "$WERF_RELEASE"

kubectl delete namespace "$WERF_NAMESPACE"
```

Delete the namespace only when it is dedicated to this demo.

## Private Registry Follow-Up

For Harbor, GHCR, or another private registry, add `imagePullSecrets` support to the Helm chart and create a namespace-scoped pull secret. Do not place registry credentials in `values.yaml` or commit them to this repository.