# Java runtime used to start the Spring Boot Visits Service.
FROM eclipse-temurin:17

WORKDIR /app

# Copy the JAR produced by `./mvnw clean verify` for this service.
COPY target/spring-petclinic-visits-service-4.0.1.jar app.jar

# Visits Service listens on this port.
EXPOSE 8082

ENTRYPOINT ["java", "-jar", "app.jar"]
