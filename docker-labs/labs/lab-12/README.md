# Lab 12: Multi-Stage Build for a Java Maven Application

This lab demonstrates how to build and run a Java Spring Boot application using a **multi-stage Docker build**.  
The first stage compiles the application using Maven, and the second stage creates a lightweight Java runtime image to run the JAR file.

---

## **1️⃣ Clone the Application Code**
```
git clone https://github.com/IbrahimAdel15/Docker1.git
cd Docker1
```
## 2️⃣ Create the Dockerfile
```
# ===== Stage 1: Build the application =====
FROM maven:3.9.6-eclipse-temurin-17 AS build

# Set working directory inside the container
WORKDIR /app

# Copy the application code into the container
COPY . .

# Build the application (this will create a JAR file in /app/target)
RUN mvn clean package -DskipTests

# ===== Stage 2: Create the runtime image =====
FROM eclipse-temurin:17-jdk

# Set working directory for runtime container
WORKDIR /app

# Copy the built JAR from the build stage
COPY --from=build /app/target/*.jar app.jar

# Expose port 9095 (application default)
EXPOSE 9095

# Run the application
ENTRYPOINT ["java", "-jar", "app.jar"]
```
## 3️⃣ Build the Docker Image
```
docker build -t multi-stage-java-app .
```
## 4️⃣ Run the Container
Mapping host port 9095 to container port 8080 (default Spring Boot port).
```
docker run -d --name java-app -p 9095:8080 multi-stage-java-app
```
## 5️⃣ Test the Application
```
curl http://localhost:9095
```
Or open in a browser:
http://localhost:9095

## 6️⃣ Stop and Remove the Container
```
docker stop java-app
docker rm java-app
```
