# Employee API - CI/CD Pipeline Project

## Overview

Employee API is a Spring Boot REST API application integrated with a complete CI/CD pipeline. This project demonstrates automated software delivery using modern DevOps practices, including continuous integration, code quality analysis, containerization, and cloud deployment.

The pipeline automates the process from source code commit to application deployment.

---

## Architecture
Developer
|
| Git Push
↓
GitHub Repository
|
↓
GitHub Webhook
|
↓
Jenkins CI/CD Pipeline
|
├── Maven Build
|
├── Unit Testing
|
├── SonarQube Code Analysis
|
---

# Technologies Used

## Application

- Java
- Spring Boot
- Maven

## DevOps Tools

- Git
- GitHub
- Jenkins
- SonarQube
- Docker
- Docker Hub
- GitHub Webhook

## Cloud Platform

- Amazon Web Services (AWS)
- EC2
- AWS ALB
- Auto Scaling Group
- EC2 Docker Containers
---

# CI/CD Pipeline Workflow

## 1. Source Code Management

- Application source code is maintained in GitHub.
- Developers push code changes to the repository.
- GitHub webhook triggers Jenkins automatically.

---

## 2. Continuous Integration with Jenkins

Jenkins automates the complete build process.

Pipeline stages:

### Environment Verification

Checks:

- Java version
- Maven version
- Docker availability

### Build Stage

Maven compiles and packages the Spring Boot application.

Command:mvn clean package

### Testing Stage

Runs automated tests.

Command:mvn test
---

# SonarQube Code Analysis

SonarQube is integrated into the Jenkins pipeline for continuous code quality monitoring.

It analyzes:

- Bugs
- Vulnerabilities
- Code Smells
- Code Duplication
- Code Quality

---

# Docker Containerization

The application is packaged as a Docker image.

## Docker Build

docker build -t employee-api .
docker run -d -p 8080:8080 employee-api


├── Docker Image Build
|
├── Docker Hub Push
|
↓
AWS EC2 Deployment
|
↓
Employee API Application

## Docker Image Publishing

The Docker image is pushed to Docker Hub for deployment.

Example:
---

# AWS Deployment

The Dockerized Employee API application is deployed on an AWS EC2 instance.

Deployment process:

1. Pull Docker image from Docker Hub.
2. Stop the previous application container.
3. Remove the old container.
4. Start the updated container.
---

# Dockerfile

Example Dockerfile:

```dockerfile
FROM eclipse-temurin:21-jdk

WORKDIR /app

COPY target/*.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java","-jar","app.jar"]
Jenkins Pipeline

The Jenkins pipeline automates:

 Source code checkout
 Maven build
 Automated testing
 SonarQube analysis
 Docker image creation
 Docker Hub publishing
 Application deployment

Future Enhancements
Prometheus and Grafana monitoring
Kubernetes deployment
Infrastructure automation using Terraform

Author

Gopika Anil


This version now shows that your project has **automatic CI triggering**, which is an important DevOps concept and looks stronger on GitHub/resume.


