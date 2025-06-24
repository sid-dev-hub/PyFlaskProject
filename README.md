# CI/CD Pipeline with Jenkins, Docker & Kubernetes

This project demonstrates a complete CI/CD pipeline for a Python app using Jenkins, Docker, Helm, and Kubernetes.

## Features
- Jenkins pipeline (code quality, build, push, deploy)
- Dockerized Python Flask app
- Helm chart for K8s deployment
- SonarQube integration

## CI/CD Flow
1. Code pushed to GitHub
2. Jenkins triggers pipeline
3. Code is analyzed by SonarQube
4. Docker image is built and pushed
5. Helm deploys to Kubernetes
