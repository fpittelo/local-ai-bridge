# Specification: Set up CI/CD Pipeline on github actions

## Overview
The goal of this track is to establish a robust CI/CD pipeline using GitHub Actions. This pipeline will automate the building and pushing of Docker images to Docker Hub, enabling remote development and deployment. The pipeline will support environment isolation for `dev`, `qa`, and `main` branches.

## Requirements
- **GitHub Actions Workflow:** Create a workflow file at `.github/workflows/ci-cd.yml`.
- **Branch Triggers:** The workflow should trigger on pushes to `dev`, `qa`, and `main` branches.
- **Environment Isolation:** Use GitHub Environments (`dev`, `qa`, `main`) to manage secrets and settings.
- **Docker Hub Integration:** Authenticate with Docker Hub using repository secrets.
- **Docker Build & Push:** Build the Docker image and push it to Docker Hub with appropriate tags (branch name and `latest` for `main`).
- **Build Arguments:** Pass `LM_HOST` and `LM_KEY` as build arguments to the Dockerfile.

## Tech Stack
- **GitHub Actions:** CI/CD orchestration.
- **Docker Hub:** Container registry.
- **Docker Buildx:** For optimized builds.

## Success Criteria
- The `.github/workflows/ci-cd.yml` file is created and correctly configured.
- Pushing to the `dev` branch triggers the workflow.
- The workflow successfully builds the Docker image and pushes it to `fredlamenace/local-ai-bridge:dev`.
- The workflow correctly identifies and uses the `dev` environment's secrets.
