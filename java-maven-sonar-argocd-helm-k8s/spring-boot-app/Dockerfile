# Build Stage: Use Maven to build the JAR file
FROM maven:3.8.6-openjdk-11 AS build
WORKDIR /app

# Copy everything into /app
COPY . .

# Change to the correct directory where pom.xml is located
WORKDIR /app/java-maven-sonar-argocd-helm-k8s/spring-boot-app

# Debug: Print the contents of the working directory
RUN ls -ltr

# Build the application, skipping tests
RUN mvn clean package -DskipTests

# Run Stage: Use a minimal Java image for production
FROM openjdk:11-jdk-slim
WORKDIR /app

# Copy only the built JAR from the previous stage
COPY --from=build /app/java-maven-sonar-argocd-helm-k8s/spring-boot-app/target/*.jar app.jar

# Expose the application port
EXPOSE 8080

# Run the Spring Boot application
CMD ["java", "-jar", "app.jar"]
