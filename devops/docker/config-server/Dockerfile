# Java runtime used to start the Spring Boot Config Server.
FROM eclipse-temurin:17

# All application files live in this directory inside the container.
WORKDIR /app

# Copy the JAR produced by `./mvnw clean verify` for this service.
COPY target/spring-petclinic-config-server-4.0.1.jar app.jar

# Config Server listens on this port. EXPOSE documents the intended port.
EXPOSE 8888

# Start the application when a container is created from this image.
ENTRYPOINT ["java", "-jar", "app.jar"]
