# Boardgame CI/CD Pipeline

This repository contains the Jenkins pipeline configuration for the "Boardgame" application. The pipeline automates the process of code checkout, compilation, testing, security analysis, and pushing the docker image to your repository.

## Pipeline Overview

The pipeline is configured as a multi-stage process, each handling a specific aspect of the software development lifecycle:

- **Git Checkout**: Clones the latest code from the main branch of the repository.
- **Compile**: Compiles the source code using Maven.
- **Test**: Executes unit tests to ensure code quality.
- **SonarQube Analysis**: Performs static code analysis to detect code smells, bugs, and security vulnerabilities.
- **OWASP Scan**: Conducts a security scan to identify known vulnerabilities in dependencies.
- **Build**: Packages the compiled code into a deployable artifact.
- **Publish to Nexus**: Deploys the artifact to a Nexus repository for sharing across development teams.
- **Build & Tag Docker Image**: Builds a Docker image and tags it.
- **Docker Image Scan**: Scans the Docker image for vulnerabilities using Trivy.
- **Push Docker Image**: Pushes the Docker image to a Docker registry.

## Tools Used

- **Jenkins**: Automation server used to execute the pipeline.
- **Maven**: Build and dependency management tool.
- **SonarQube**: Tool for continuous inspection of code quality.
- **OWASP Dependency Check**: Utility that identifies project dependencies and checks if there are any known vulnerabilities.
- **Docker**: Platform for developing, shipping, and running applications.
- **Trivy**: A simple and comprehensive vulnerability scanner for containers and other artifacts.

## Jenkins Plugins 

- **Eclipse Temurin Installer**: Installs Eclipse Temurin JDK for builds requiring Java. Useful for ensuring a specific version of Java is used during the build process.
- **Pipeline Maven Integration**: Integrates Maven with Pipeline, providing efficient handling of Maven goals and configuration in Jenkins pipelines.
- **Config File Provider**: Manages configuration files used within the Jenkins environment. This can include files like settings.xml for Maven, JSON, and other config formats, which are made available to builds via the workspace.
- **SonarQube Scanner**: Facilitates the integration of SonarQube analysis into Jenkins jobs. This plugin ensures that the code quality checks and security scans performed by SonarQube are automatically part of the CI process.
- **OWASP Dependency-Check**: Provides a mechanism to use the OWASP Dependency Check tool within Jenkins. This tool scans project dependencies for known vulnerabilities and integrates the findings into the Jenkins build logs.
- **Docker**: Allows Jenkins to build and use Docker containers within the CI/CD process. Essential for jobs which involve Docker operations like building images or running containers.
- **Docker Pipeline Step**: Adds specific steps for managing Docker operations directly within Pipeline scripts. It supports commands like building, running, and pushing Docker containers, crucial for Docker-based CI/CD pipelines.

## Jenkins Setup

The Jenkins pipeline is defined in the `Jenkinsfile` which is configured to use:
- JDK 17
- Maven 3
- Sonar Scanner
- Docker

## Running the Pipeline

To run this pipeline:
1. Ensure Jenkins is setup with the necessary plugins and configurations as per the `Jenkinsfile`.
2. Trigger a build through Jenkins' UI by clicking on 'Build Now'.
3. Monitor the build progress and output directly on Jenkins.