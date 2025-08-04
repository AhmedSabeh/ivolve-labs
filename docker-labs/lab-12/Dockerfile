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

# Expose port 8080 (application default)
EXPOSE 8080

# Run the application
ENTRYPOINT ["java", "-jar", "app.jar"]

