### XOps Microchallenge #6 – CI/CD + Kubernetes with GitHub Actions & Argo CD
Objective

## Build a CI/CD pipeline that:

Builds and pushes a Docker image of your app to Docker Hub

Updates Kubernetes manifests with the new image version

Uses Argo CD to automatically sync and deploy your app into your local kind cluster

### Prerequisites

Docker installed and running

kind CLI installed

kubectl installed

### GitHub account with push access

Docker Hub account with credentials stored in GitHub Secrets (DOCKER_USERNAME, DOCKER_PASSWORD)

# Step 1: Prepare Your App Repo

Use a simple app (NGINX, static site, Python app, or Node.js app)

Ensure there is a working Dockerfile

Push the app to a GitHub repository

# Step 2: Set Up Kubernetes Manifests Repo (Infra Repo)

Create a second repository to hold Kubernetes manifests

# Include:

deployment.yaml

service.yaml

README.md

Ensure deployment.yaml references the Docker image pushed by GitHub Actions

# Infra Repo Notes:

Deployment image: <DOCKER_USERNAME>/myapp:<tag>

Service exposes NodePort 30080

Argo CD should point to this repo and path k8s/

Step 3: Build & Push with GitHub Actions

Create a workflow in .github/workflows to automate the CI/CD process

# Workflow should:

Build a Docker image of the app

Push the image to Docker Hub

Checkout the Infra Repo

Update deployment manifests with the new image

Commit and push changes to the Infra Repo

Store Docker Hub credentials in GitHub Secrets

# Step 4: Install Argo CD on kind Cluster

Install Argo CD in the kind cluster

Configure Argo CD to point to the Infra Repo

Enable auto-sync for continuous deployment

# Step 5: Trigger Deployment

Push new code to the App Repo

GitHub Actions builds and pushes the Docker image

Deployment manifests are updated in the Infra Repo

Argo CD automatically syncs and deploys the new version

Verify the app is running on the Kubernetes cluster
