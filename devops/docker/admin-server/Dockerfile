# Java runtime used to start the Spring Boot Admin Server.
FROM eclipse-temurin:17

WORKDIR /app

# Copy the JAR produced by `./mvnw clean verify` for this service.
COPY target/spring-petclinic-admin-server-4.0.1.jar app.jar

# Admin Server listens on this port.
EXPOSE 9090

ENTRYPOINT ["java", "-jar", "app.jar"]
