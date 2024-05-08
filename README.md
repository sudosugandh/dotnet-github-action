# GitHub Actions Workflow

This repository utilizes GitHub Actions for Continuous Integration (CI) and Continuous Deployment (CD) workflows. Below is an overview of the workflow steps:

## CI Workflow (docker-cd)

The CI workflow is triggered on every push to the master branch. It performs the following tasks:

1. **Checkout**: Clones the repository.
2. **Docker Login**: Logs in to Docker Hub using the provided credentials.
3. **Environment Setup**: Checks if the .env file exists and copies .env.sample if not present.
4. **Build Images**: Builds Docker images using docker-compose with the --no-cache option.
5. **Docker Push**: Pushes the built Docker images to the Docker Hub repository.

## CD Workflow (deploy)

The CD workflow is triggered after the successful completion of the CI workflow. It performs the following tasks:

1. **Checkout**: Clones the repository.
2. **SSH into Server**: Uses SSH to connect to the deployment server.
3. **Pull Updates**: Pulls the latest changes from the master branch of the repository on the deployment server.
4. **Remove Local Images**: Removes existing Docker images on the deployment server.
5. **Build and Deploy**: Builds Docker images with --pull and --no-cache options, and then deploys the application using docker-compose.

## Workflow Configuration

```yaml
name: docker-cd
on:
  push:
    branches:
      - master

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      # Steps for CI workflow

  deploy:
    needs: build
    runs-on: ubuntu-latest
    steps:
      # Steps for CD workflow

## Usage

1. Clone the repository:

   ```bash
   git clone https://github.com/sudosugandh/dotnet-github-action.git
