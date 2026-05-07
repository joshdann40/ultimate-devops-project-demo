# Utlimate DevOps Project Demo

Production-style DevOps portfolio project for deploying and operating a
microservices application with Docker, Kubernetes, GitHub Actions, reverse
proxying, and OpenTelemetry-based observability.

> Fork disclosure: this repository is based on
> `iam-veeramalla/ultimate-devops-project-demo`, which itself is based on the
> OpenTelemetry Astronomy Shop demo. My work focuses on DevOps engineering:
> documentation, CI/CD, deployment flow, reverse proxy architecture, operations,
> and portfolio-ready project ownership.

## Why this project exists

This project is designed to show practical DevOps skills on top of a realistic
microservices system. Instead of a small single-service demo, it uses a larger
distributed application with many moving parts, which creates a better surface
for deployment, automation, troubleshooting, and observability work.

## DevOps skills demonstrated

- Container-based local development with Docker Compose.
- Kubernetes deployment structure using separate service manifests.
- Reverse proxy entrypoint with Envoy for routing frontend and platform traffic.
- GitHub Actions CI for build, test, lint, Docker image publishing, and manifest
  updates.
- Multi-service architecture awareness across frontend, backend, data,
  messaging, and support services.
- Operational documentation through runbooks, architecture notes, and change
  tracking.
- Clean fork attribution and project ownership without misrepresenting upstream
  application code.

## Architecture summary

The application is a distributed e-commerce demo. A frontend service communicates
with backend services for product catalog, cart, checkout, payment, shipping,
currency, recommendations, ads, email, accounting, and fraud detection.

Platform components include Kafka, Valkey, feature flags, load generation,
OpenTelemetry collectors, and a frontend reverse proxy.

The reverse proxy is important because it acts as the single entrypoint for user
traffic and routes requests to internal services. In Kubernetes, ingress traffic
targets the `opentelemetry-demo-frontendproxy` service, keeping internal service
addresses away from external users.

More detail:

- [Architecture notes](docs/ARCHITECTURE.md)
- [Runbook](docs/RUNBOOK.md)
- [My work log](docs/MY-WORK.md)

## Repository layout

```text
.
|-- .github/workflows/        # GitHub Actions CI workflow
|-- docker-compose.yml        # Full local multi-service environment
|-- docker-compose.minimal.yml # Smaller local environment
|-- kubernetes/               # Kubernetes deployment and service manifests
|-- src/                      # Microservice source code
|-- docs/                     # Portfolio documentation and runbooks
|-- pb/                       # Shared protobuf definitions
`-- test/                     # Test and validation assets
```

## CI/CD workflow

The current workflow targets the product catalog service and performs:

1. Go build.
2. Unit tests.
3. Go linting.
4. Docker image build and push.
5. Kubernetes deployment image tag update.

To use the Docker publishing step, configure these repository secrets:

- `DOCKER_USERNAME`
- `DOCKER_TOKEN`

The workflow is intentionally scoped to one service first. That makes it easier
to demonstrate a clean CI/CD path before expanding the same pattern to the rest
of the platform.

## Local quick start

Start the complete stack:

```bash
docker compose up --build
```

Start the smaller stack:

```bash
docker compose -f docker-compose.minimal.yml up --build
```

Check running containers:

```bash
docker compose ps
```

Stop the environment:

```bash
docker compose down
```

## Kubernetes quick start

Apply the Kubernetes resources:

```bash
kubectl apply -f kubernetes/serviceaccount.yaml
kubectl apply -f kubernetes/
```

Check workloads:

```bash
kubectl get pods
kubectl get svc
kubectl get deploy
```

The Kubernetes ingress in `kubernetes/frontendproxy/ingress.yaml` routes
external HTTP traffic to the frontend proxy service.

## What I changed after forking

- Reworked the README into a portfolio-grade project overview.
- Added architecture documentation.
- Added an operational runbook.
- Added a personal work log with next improvements and interview talking points.
- Cleaned GitHub Actions bot attribution.
- Added Windows metadata ignores.
- Documented the reverse proxy role clearly for reviewers and interviews.

## Planned improvements

- Rename the repository to a shorter resume-friendly URL.
- Add screenshots of the local app and observability views.
- Add Kubernetes namespace and environment overlays.
- Add resource requests and limits to selected workloads.
- Add GitOps deployment with Argo CD or Flux.
- Expand CI/CD beyond the product catalog service.
- Add smoke tests for the frontend and key APIs.

## Resume summary

DevOps portfolio project based on a forked OpenTelemetry microservices demo;
customized CI/CD, Docker Compose, Kubernetes manifests, reverse proxy routing,
and operational documentation to demonstrate deployment and platform engineering
skills.

## Attribution and license

This repository is a fork-based portfolio project. Original project sources:

- `iam-veeramalla/ultimate-devops-project-demo`
- OpenTelemetry Demo / Astronomy Shop

The original OpenTelemetry Demo is licensed under Apache 2.0. This repository
keeps the original license and attribution intact while documenting my DevOps
customization work separately.
