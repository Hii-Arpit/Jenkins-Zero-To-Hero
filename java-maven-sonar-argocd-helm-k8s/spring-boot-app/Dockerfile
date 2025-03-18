# Build Stage: Use Maven to build the JAR file
FROM maven:3.8.6-openjdk-11 AS build
WORKDIR /app

# Copy the project files
COPY . .

# Build the application, skipping tests for faster build
RUN mvn clean package -DskipTests

# Run Stage: Use a minimal Java image for production
FROM openjdk:11-jdk-slim
WORKDIR /app

# Copy only the built JAR from the previous stage
COPY --from=build /app/target/spring-boot-web.jar app.jar

# Expose the application port
EXPOSE 8080

# Run the Spring Boot application
CMD ["java", "-jar", "app.jar"]
