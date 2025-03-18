# Build Stage: Use Maven to build the JAR file
FROM maven:3.8.6-openjdk-11 AS build
WORKDIR /app

# Copy everything from the correct location
COPY . .

# Debugging step: List files in /app to verify pom.xml is present
RUN ls -ltr /app

# Build the application, skipping tests for faster build
RUN mvn clean package -DskipTests

# Run Stage: Use a minimal Java image for production
FROM openjdk:11-jdk-slim
WORKDIR /app

# Copy only the built JAR from the previous stage
COPY --from=build /app/target/*.jar app.jar

# Expose the application port
EXPOSE 8080

# Run the Spring Boot application
CMD ["java", "-jar", "app.jar"]
