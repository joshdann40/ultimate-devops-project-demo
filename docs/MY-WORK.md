# My Work Log

This file tracks the changes I made after duplicating the upstream demo into my
own GitHub repository.

## Completed

- Created a personal GitHub repository named `utlimate-devops-project-demo`.
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

## Next Improvements

- Run the project locally with Docker Compose and add screenshots.
- Deploy the Kubernetes manifests to a local cluster and document the result.
- Add resource requests and limits to selected services.
- Add namespace support for cleaner Kubernetes deployment.
- Add a GitOps workflow using Argo CD or Flux.
- Expand CI checks beyond the product catalog service.

## Interview Talking Points

- I used an existing open-source microservices demo as the base, then adapted it
  into a personal DevOps project.
- I can explain the service topology, deployment options, and CI workflow.
- I can explain how the Envoy frontend proxy acts as the application entrypoint
  in both Docker Compose and Kubernetes.
- I understand the difference between application code ownership and DevOps
  ownership: my focus is packaging, deployment, validation, and operations.
- I kept attribution and licensing intact while making the project easier to
  review as part of my portfolio.
