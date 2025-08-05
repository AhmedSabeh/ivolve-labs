# Lab 11 — Run Java Spring Boot App in a Docker Container

## 📌 Objective
This lab demonstrates how to run a Java Spring Boot application inside a Docker container using **Maven** and **Java 17**.  
We will explore **two approaches**:
1. **Option A** — Build the application inside the container.
2. **Option B** — Build the application locally before creating the container.

---

## 📂 Table of Contents
1. [Clone the Repository](#1-clone-the-repository)
2. [Option A: Build Inside Container](#2-option-a-build-inside-container)
3. [Option B: Build Locally First](#3-option-b-build-locally-first)
4. [Testing the Application](#4-testing-the-application)
5. [Stopping & Removing Containers](#5-stopping--removing-containers)
6. [Notes](#6-notes)

---

## 1️⃣ Clone the Repository
```
git clone https://github.com/IbrahimAdel15/Docker1.git
cd Docker1
```
2️⃣ Option A: Build Inside Container
Step 1: Create Dockerfile
```
# Use Maven with Java 17
FROM maven:3.9.6-eclipse-temurin-17

# Set working directory
WORKDIR /app

# Copy application source code
COPY . .

# Build the application
RUN mvn package

# Expose application port
EXPOSE 9092

# Run the Spring Boot application
CMD ["java", "-jar", "target/demo-0.0.1-SNAPSHOT.jar"]
```
Step 2: Build the Image
```
docker build -t springboot-docker:latest .
```
Step 3: Run the Container
```
docker run -d --name springboot-container -p 9092:9092 springboot-docker:latest
```
3️⃣ Option B: Build Locally First
Step 1: Build the Application Locally
```
mvn clean package
```
Step 2: Create Dockerfile
```
# Use Java 17 base image
FROM eclipse-temurin:17-jdk

# Set working directory
WORKDIR /app

# Copy the pre-built JAR file from local machine
COPY target/demo-0.0.1-SNAPSHOT.jar app.jar

# Expose application port
EXPOSE 9092

# Run the Spring Boot application
CMD ["java", "-jar", "app.jar"]
```
Step 3: Build the Image
```
docker build -t springboot-docker:latest .
```
Step 4: Run the Container
```
docker run -d --name springboot-container -p 9092:9092 springboot-docker:latest
```
4️⃣ Testing the Application
Using curl:
```
curl http://localhost:9092
```
Or open in a browser:

http://localhost:9092

5️⃣ Stopping & Removing Containers
```
docker stop springboot-container
docker rm springboot-container
```
6️⃣ Notes
Option A: Builds the application inside the Docker image. Useful for CI/CD pipelines.

Option B: Builds the application locally, then copies the JAR file. Faster for local development.

Ensure port 9092 is free before running the container.

Change springboot-docker:latest to another tag if you want to version your images.
