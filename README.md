# Boardgame CI/CD Pipeline

This repository contains the Jenkins pipeline configuration for the "Boardgame" application. The pipeline automates the process of code checkout, compilation, testing, security analysis, and deployment using a Jenkins Agent.

## Pipeline Overview

The pipeline is configured as a multi-stage process, each handling a specific aspect of the software development lifecycle:

- **Git Checkout**: Clones the latest code from the main branch of the repository.
- **Compile**: Compiles the source code using Maven.
- **Test**: Executes unit tests to ensure code quality.
- **SonarQube Analysis**: Performs static code analysis to detect code smells, bugs, and security vulnerabilities.
- **Build**: Packages the compiled code into a deployable artifact.
- **OWASP Scan**: Conducts a security scan to identify known vulnerabilities in dependencies.
- **Publish to Nexus**: Deploys the artifact to a Nexus repository for sharing across development teams.
- **Build & Tag Docker Image**: Builds a Docker image and tags it.
- **Docker Image Scan**: Scans the Docker image for vulnerabilities using Trivy.
- **Push Docker Image**: Pushes the Docker image to a Docker registry.
- **Docker Deploy**: Deploys the Docker image to a production-like environment.

## Tools Used

- **Jenkins**: Automation server used to execute the pipeline.
- **Maven**: Build and dependency management tool.
- **SonarQube**: Tool for continuous inspection of code quality.
- **OWASP Dependency Check**: Utility that identifies project dependencies and checks if there are any known vulnerabilities.
- **Docker**: Platform for developing, shipping, and running applications.
- **Trivy**: A simple and comprehensive vulnerability scanner for containers and other artifacts.

## Jenkins Setup

The Jenkins pipeline is defined in the `Jenkinsfile` which is configured to use:
- JDK 17
- Maven 3
- Sonar Scanner
- Docker

## Running the Pipeline

To run this pipeline:
1. Ensure Jenkins is setup with necessary plugins and configurations as per the `Jenkinsfile`.
2. Trigger a build through Jenkins' UI by clicking on 'Build Now'.
3. Monitor the build progress and output directly on Jenkins.