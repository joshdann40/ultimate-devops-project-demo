# Runbook

This runbook captures the commands I would use to operate and validate the demo
locally or in a Kubernetes cluster.

## Prerequisites

- Docker Desktop or a compatible Docker engine.
- Docker Compose v2.
- `kubectl` for Kubernetes deployment.
- Access to a Kubernetes cluster such as Docker Desktop Kubernetes, minikube, or
  kind.
- GitHub repository secrets for image publishing:
  - `DOCKER_USERNAME`
  - `DOCKER_TOKEN`

## Local Docker Compose

Start the complete stack:

```bash
docker compose up --build
```

Start the minimal stack:

```bash
docker compose -f docker-compose.minimal.yml up --build
```

Check containers:

```bash
docker compose ps
```

Follow logs:

```bash
docker compose logs -f
```

Stop the stack:

```bash
docker compose down
```

## Kubernetes Deployment

Apply the service account and manifests:

```bash
kubectl apply -f kubernetes/serviceaccount.yaml
kubectl apply -f kubernetes/
```

Check workload health:

```bash
kubectl get pods
kubectl get svc
kubectl get deploy
```

Inspect a failing pod:

```bash
kubectl describe pod <pod-name>
kubectl logs <pod-name>
```

Restart a deployment:

```bash
kubectl rollout restart deployment/<deployment-name>
```

Check rollout status:

```bash
kubectl rollout status deployment/<deployment-name>
```

## CI Validation

The GitHub Actions workflow validates the product catalog service. Local
equivalent commands:

```bash
cd src/product-catalog
go mod download
go build -o product-catalog-service main.go
go test ./...
```

## Common Issues

## Docker Compose port conflicts

If a service fails to start because a port is already in use, stop the process
using that port or adjust the compose file for a local-only override.

## Kubernetes image pull errors

Confirm that the image tag exists in the container registry and that the cluster
has access to pull it.

## CI Docker push failure

Confirm `DOCKER_USERNAME` and `DOCKER_TOKEN` are configured in repository
secrets and that the token has permission to push images.

## Product catalog deployment not updating

Check whether the CI workflow committed the updated image tag to
`kubernetes/productcatalog/deploy.yaml`, then verify the cluster has applied the
latest manifest.
