# Use Java 17 base image
FROM eclipse-temurin:17-jdk

# Create working directory
WORKDIR /app

# Copy the pre-built JAR file from local machine
COPY target/demo-0.0.1-SNAPSHOT.jar app.jar

# Expose the application port
EXPOSE 9092

# Run the Spring Boot application
CMD ["java", "-jar", "app.jar"]

