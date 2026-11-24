# Hello DevOps – Module 05

## Project Overview

Hello DevOps is a simple Python Flask web application developed as part of the Codomax Cloud and DevOps internship, Module 05: DevOps, CI/CD & Monitoring.

The project demonstrates automated software testing, Docker image building, publishing to GitHub Container Registry, local deployment and application health monitoring.

## Technologies Used

- Python 3.12
- Flask
- Pytest
- Git and GitHub
- GitHub Actions
- Docker
- GitHub Container Registry (GHCR)

## Application Features

The application provides two endpoints:

| Endpoint | Description |
|---|---|
| `/` | Displays the Hello DevOps welcome page and application version |
| `/health` | Returns the application's health status |

Example health response:

```json
{"status": "healthy"}
```

## Project Structure

```text
hello-devops/
├── .github/
│   └── workflows/
│       └── ci.yml
├── tests/
│   └── test_app.py
├── app.py
├── requirements.txt
├── Dockerfile
├── .gitignore
└── README.md
```

## Continuous Integration and Delivery

GitHub Actions automates the project's CI/CD workflow.

When code is pushed to the `main` branch:

1. GitHub Actions retrieves the source code.
2. Python 3.12 is configured.
3. Application dependencies are installed.
4. Automated tests are executed using Pytest.
5. Docker Buildx prepares the image-building environment.
6. A Docker image is built.
7. The image is published to GitHub Container Registry.

The Docker image is only published after the automated tests pass.

Pull requests targeting `main` also trigger the workflow, but do not publish an image.

## Automated Testing

The project includes two automated tests:

- Home page test: verifies that the application returns HTTP 200 and displays the expected welcome message.
- Health endpoint test: verifies that the health endpoint returns HTTP 200 and the expected healthy status.

Both tests passed locally and through GitHub Actions.

## Docker Image and Deployment

The Docker image is published to:

`ghcr.io/nompumelelo1g/hello-devops:latest`

To download the image:

```bash
sudo docker pull ghcr.io/nompumelelo1g/hello-devops:latest
```

To run the application:

```bash
sudo docker run -d -p 8081:5000 --name hello-devops ghcr.io/nompumelelo1g/hello-devops:latest
```

The application can then be accessed at:

- http://localhost:8081
- http://localhost:8081/health

Deployment to the local machine is performed manually after the image has been published.

## Monitoring

Monitoring is demonstrated through:

- Application health endpoint (`/health`).
- Docker container logs.
- Docker container status.
- Docker HEALTHCHECK instruction.

The Docker health check periodically sends a request to the application's health endpoint.

To inspect the container:

```bash
sudo docker ps
```

To view application logs:

```bash
sudo docker logs hello-devops
```

To inspect the health status:

```bash
sudo docker inspect --format='{{.State.Health.Status}}' hello-devops
```

A successful health check reports:

`healthy`

## Learning Outcomes

Through this project, the following DevOps concepts were demonstrated:

- Version control and GitHub workflows.
- Continuous Integration.
- Automated testing.
- Docker image creation and containerisation.
- Continuous Delivery through automated image publishing.
- Local application deployment.
- Application and container health monitoring.

## Repository

[Hello DevOps – GitHub Repository](https://github.com/nompumelelo1g/codomax-module-05-devops)

Developed as part of the Codomax Cloud and DevOps Internship – Module 05.
