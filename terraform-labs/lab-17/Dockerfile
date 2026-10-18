# Use Maven base image
FROM maven:3.9.4-eclipse-temurin-17 AS build

# Set working directory
WORKDIR /app

# Copy application code
COPY . .

# Build the application
RUN mvn package -DskipTests

# Use a lightweight JDK base image for runtime
FROM eclipse-temurin:17-jdk

WORKDIR /app

# Copy the built jar from the build stage
COPY --from=build /app/target/demo-0.0.1-SNAPSHOT.jar app.jar

# Expose application port
EXPOSE 5050

# Run the application
ENTRYPOINT ["java", "-jar", "app.jar"]

