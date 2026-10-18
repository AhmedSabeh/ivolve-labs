# Lab 17: Container Image Vulnerability Scanning Using Trivy

## Objective

This lab demonstrates how to:

- Install and use [Trivy](https://trivy.dev/latest/getting-started/installation) to scan Docker images for vulnerabilities.
- Containerize a Java application using a Maven base image.
- Scan the image and generate a vulnerability report in JSON format.
- Push the scanned image to DockerHub.

---

## Prerequisites

- Docker installed and running.
- Git installed.
- Maven installed (optional, for local testing).
- DockerHub account.
- Trivy installed ([Installation Guide](https://trivy.dev/latest/getting-started/installation)).

---

## Steps

### 1. Clone the Application Repository

```
git clone https://github.com/Ibrahim-Adel15/Docker-1.git
cd Docker-1
```
Note: The repo contains the Java application source code.

### 2. Create Dockerfile
Create a Dockerfile in the project root with the following content:
```
# Use Maven base image
FROM maven:3.8.6-openjdk-17 AS build

# Set working directory
WORKDIR /app

# Copy the application code
COPY . .

# Build the application
RUN mvn clean package

# Create the final image using a smaller base
FROM openjdk:17-jdk-slim

WORKDIR /app

# Copy the jar from the build stage
COPY --from=build /app/target/demo-0.0.1-SNAPSHOT.jar app.jar

# Expose the application port
EXPOSE 5050

# Run the application
ENTRYPOINT ["java", "-jar", "app.jar"]
```
### 3. Build the Docker Image
```
docker build -t your-dockerhub-username/demo-app:latest .
```
### 4. Scan the Docker Image Using Trivy
```
trivy image -f json -o trivy-report.json your-dockerhub-username/demo-app:latest
```
This will generate a detailed JSON report saved as trivy-report.json.

### 5. Push Image to DockerHub
```
docker login
docker push your-dockerhub-username/demo-app:latest
```
