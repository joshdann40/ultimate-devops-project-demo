# Utlimate DevOps Project Demo

A portfolio DevOps project based on the OpenTelemetry Astronomy Shop demo. This
repository is my working version of a production-style microservices platform:
containerized services, Kubernetes manifests, GitHub Actions CI, and
observability-focused runtime configuration.

## What this project demonstrates

- Multi-service application deployment with Docker Compose and Kubernetes.
- CI for the product catalog service, including build, unit test, lint, image
  build, and Kubernetes manifest update steps.
- Service-to-service architecture using several implementation languages.
- Practical observability concepts with OpenTelemetry instrumentation.
- A maintainable project structure that can be extended for cloud deployment,
  monitoring, and GitOps workflows.

## My customization work

This repo started from an existing open-source demo, then I adapted it into a
personal DevOps portfolio project. My current changes focus on making the
project understandable, reviewable, and ready for further hands-on deployment
work.

- Reframed the README around DevOps portfolio usage.
- Added project-specific architecture notes in `docs/ARCHITECTURE.md`.
- Added a hands-on runbook in `docs/RUNBOOK.md`.
- Added a personal change log in `docs/MY-WORK.md`.
- Cleaned the CI bot identity so automated commits are not attributed to the
  original tutorial author.
- Added Windows metadata ignores for a cleaner working tree.

## Architecture at a glance

The application is a distributed e-commerce demo. The frontend talks to backend
services for product catalog, cart, checkout, currency, payment, shipping,
recommendations, advertising, and related support services. Supporting
infrastructure includes Kafka, Valkey, feature flags, load generation, and
OpenTelemetry components.

See `docs/ARCHITECTURE.md` for the fuller service map and deployment notes.

## Local quick start

Docker is the fastest way to run the full environment locally:

```bash
docker compose up --build
```

For a smaller local stack:

```bash
docker compose -f docker-compose.minimal.yml up --build
```

Kubernetes manifests are available under `kubernetes/`. See `docs/RUNBOOK.md`
for suggested validation commands and troubleshooting notes.

## CI/CD

The workflow in `.github/workflows/ci.yaml` currently targets the
`src/product-catalog` service. It performs:

1. Go dependency download and build.
2. Unit tests.
3. Go linting.
4. Docker image build and push.
5. Kubernetes deployment image tag update.

To use the Docker push step, configure these repository secrets:

- `DOCKER_USERNAME`
- `DOCKER_TOKEN`

## Roadmap

- Add a Kubernetes namespace and environment overlay for a personal deployment.
- Add screenshots of a successful local run and observability views.
- Add service health checks and resource requests/limits where missing.
- Add a GitOps deployment path with Argo CD or Flux.
- Add a short incident runbook for common service failures.

## Attribution

This project is based on:

- `iam-veeramalla/ultimate-devops-project-demo`
- The OpenTelemetry Demo / Astronomy Shop project

The original OpenTelemetry Demo is licensed under Apache 2.0. I am keeping the
license and attribution intact while using this repository as a personal DevOps
learning and portfolio project.
