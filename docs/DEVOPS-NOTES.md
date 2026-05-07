# DevOps Notes

This file tracks the DevOps-focused changes made after duplicating the upstream
demo into my own GitHub repository.

## Completed

- Created a personal GitHub repository named `ultimate-devops-project-demo`.
- Preserved the original project history and kept the original repository as
  `upstream`.
- Rewrote the root README so the project is presented as a DevOps portfolio
  project instead of an untouched upstream copy.
- Added architecture notes that explain the services and platform components.
- Added a runbook with local Docker, Kubernetes, and CI validation commands.
- Updated CI attribution to use the GitHub Actions bot identity.
- Ignored Windows `desktop.ini` metadata files.
- Strengthened the README with fork disclosure, resume summary, reverse proxy
  explanation, and clearer DevOps ownership.

## Evidence To Add

- Docker Compose local run screenshot.
- Grafana or observability dashboard screenshot.
- Kubernetes pod status screenshot from a local cluster.

## Next Improvements

- Add resource requests and limits to selected services.
- Add namespace support for cleaner Kubernetes deployment.
- Add a GitOps workflow using Argo CD or Flux.
- Expand CI checks beyond the product catalog service.

## Interview Discussion Notes

- I used an existing open-source microservices demo as the base, then adapted it
  into a personal DevOps project.
- I can explain the service topology, deployment options, and CI workflow.
- I can explain how the Envoy frontend proxy acts as the application entrypoint
  in both Docker Compose and Kubernetes.
- I understand the difference between application code ownership and DevOps
  ownership: my focus is packaging, deployment, validation, and operations.
- I kept attribution and licensing intact while making the project easier to
  review as part of my portfolio.
