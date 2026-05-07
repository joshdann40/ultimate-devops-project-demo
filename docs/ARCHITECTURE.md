# Architecture Notes

This project is a fork-based microservices demo adapted into a DevOps portfolio
project. The main value is not claiming ownership of the original application
code. The value is showing how a realistic distributed system is packaged,
deployed, routed, observed, and documented.

## Service Groups

## User-Facing Layer

- `frontend`: web application used by shoppers.
- `frontendproxy`: entrypoint/proxy service for frontend traffic.
- `flagd-ui`: UI for feature flag management.

## Business Services

- `product-catalog`: product listing and lookup.
- `cart`: cart storage and cart operations.
- `checkout`: checkout orchestration.
- `payment`: payment handling.
- `shipping`: shipping quote and order shipment flow.
- `currency`: currency conversion.
- `recommendation`: product recommendation flow.
- `ad`: ad service.
- `email`: confirmation email service.
- `accounting`: accounting event consumer.
- `fraud-detection`: fraud detection event consumer.

## Platform Services

- `kafka`: event streaming backbone.
- `valkey`: cart data store.
- `flagd`: feature flag service.
- `loadgenerator`: synthetic traffic generator.
- OpenTelemetry components configured through the compose and manifest files.

## Reverse Proxy

The `frontendproxy` component is the public entrypoint for the application. It
uses Envoy to route traffic to the frontend and related platform endpoints.

In Docker Compose, the service is named `frontend-proxy` and exposes the Envoy
listener and admin ports from environment variables.

In Kubernetes, the service is named `opentelemetry-demo-frontendproxy`. The
ingress manifest forwards external HTTP traffic to this service on port `8080`.
This keeps internal services behind the cluster network and gives the platform a
single routing point for external access.

This is useful in a DevOps context because a reverse proxy can centralize:

- External routing.
- Path-based service access.
- TLS termination when configured with a real ingress controller.
- Traffic policy.
- Observability at the edge of the application.

## Deployment Layout

The repository supports two main deployment styles:

- Docker Compose for local development and quick demonstrations.
- Kubernetes manifests under `kubernetes/` for cluster deployment.

The Kubernetes layout keeps service manifests in separate directories, which
makes it easier to review and evolve individual services without touching the
whole platform at once.

## CI/CD Focus

The current GitHub Actions workflow focuses on the product catalog service. That
is a practical first CI target because it has a clear build and test path, and
its container image can be pushed and referenced from the Kubernetes deployment
manifest.

Future improvements should expand the same pattern to other services:

- Build and test each service independently.
- Publish service images with immutable tags.
- Update Kubernetes manifests or GitOps image policies.
- Run smoke tests against a temporary environment.

## Operational Skills Shown

- Reading and organizing a multi-service codebase.
- Understanding container build contexts.
- Managing Kubernetes deployment and service manifests.
- Wiring CI to tests, image publishing, and deployment manifest updates.
- Explaining the reverse proxy as the external entrypoint.
- Preserving upstream attribution while making project-specific changes.
