# GitLab CI/CD Pipeline for Kubernetes Deployment

A multi-environment CI/CD pipeline built with GitLab CI/CD, Docker, Amazon Elastic Container Registry (ECR), and Kubernetes.

This project demonstrates an automated application build and deployment workflow designed to support multiple environments, from development to production.

## Overview

The pipeline automates the application build process, creates Docker images, pushes them to Amazon ECR, and deploys the images to Kubernetes clusters.

Each environment has its own deployment configuration to ensure proper separation and controlled release management.

### Technology Stack

- **GitLab CI/CD** – Pipeline automation and deployment orchestration.
- **Docker** – Application containerization.
- **Amazon ECR** – Docker image registry.
- **Kubernetes** – Container orchestration and application deployment.
- **Go** – Application build example.

## Architecture

```text
                 GitLab Repository
                        |
                        v
                 GitLab CI/CD
                        |
                  Build Go App
                        |
                        v
                  Docker Build
                        |
                        v
                  Amazon ECR
                        |
                        v
              Kubernetes Deployment
                        |
        +---------------+---------------+
        |               |               |
        v               v               v
   Development       Staging           UAT
   (Automatic)      (Automatic)     (Automatic)
                                        |
                                        v
                                  Production
                                    (Manual)
```

## Deployment Workflow

The pipeline uses Git branches to determine the target deployment environment.

| Git Branch | Environment | Deployment |
|---|---|---|
| `dev` | Development | Automatic |
| `staging` | Staging | Automatic |
| `uat` | UAT | Automatic |
| `master` | Production | Manual trigger |

### Pipeline Execution Steps

Each deployment job performs the following operations:

1. **Build Application** – Compile the Go application.
2. **Build Docker Image** – Package the application into a Docker image.
3. **Image Tagging** – Generate a unique image tag using the GitLab pipeline ID.
4. **Push to Amazon ECR** – Upload the Docker image to the container registry.
5. **Select Kubernetes Environment** – Load the corresponding Kubernetes configuration.
6. **Deploy Application** – Update the Kubernetes Deployment with the newly built image.
7. **Docker Image Cleanup** – Remove the local Docker image after deployment.

## Environment Separation

Each environment uses a dedicated Kubernetes configuration file.

- Development: `config_dev`
- Staging: `config_staging`
- UAT: `config_uat`
- Production: `config_production`

This approach helps maintain environment isolation and ensures deployments target the intended Kubernetes cluster.

## Production Release Strategy

Production deployments require a manual trigger through GitLab CI/CD.

This provides an additional release control step before changes are deployed to the production environment.

The workflow allows the team to validate application changes in Development, Staging, and UAT before promoting them to Production.

## Key Features

- Automated CI/CD workflows using GitLab Community Edition.
- Docker-based application packaging.
- Centralized container image storage using Amazon ECR.
- Kubernetes deployments across four environments.
- Unique Docker image tags based on GitLab pipeline IDs.
- Environment-specific Kubernetes configurations.
- Controlled production deployment through manual execution.
- Automated cleanup of local Docker images after deployment.

## Prerequisites

Before running the pipeline, the following components must be available:

- A GitLab repository with CI/CD enabled.
- A GitLab Runner configured with the required execution environment.
- Docker installed on the runner.
- AWS credentials and permissions to push images to Amazon ECR.
- Kubernetes cluster access for each deployment environment.
- `kubectl` installed and configured on the runner.
- A Go application with a valid Dockerfile.

## Security Considerations

For production use, sensitive credentials and configuration files should be managed through GitLab CI/CD variables or a secure secrets management solution.

Kubernetes access should follow the principle of least privilege, with deployment permissions restricted to the appropriate environments.

Never commit AWS credentials, Kubernetes configuration files, access tokens, or other sensitive information to the repository.

## Project Purpose

This pipeline represents practical DevOps experience in building and maintaining automated deployment workflows for cloud-native applications.

It was developed collaboratively as part of a DevOps team, with a focus on deployment consistency, environment separation, operational efficiency, and controlled production releases.

**Project:** GitLab CI/CD for Kubernetes Deployment
