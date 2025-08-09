# Use Maven with Java 17
FROM maven:3.9.6-eclipse-temurin-17

# Create working directory
WORKDIR /app

# Copy application source code
COPY . .

# Build the application
RUN mvn package

# Expose the application port
EXPOSE 9092

# Run the Spring Boot application
CMD ["java", "-jar", "target/demo-0.0.1-SNAPSHOT.jar"]

