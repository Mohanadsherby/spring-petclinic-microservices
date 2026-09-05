# Java runtime used to start the Spring Boot Vets Service.
FROM eclipse-temurin:17

WORKDIR /app

# Copy the JAR produced by `./mvnw clean verify` for this service.
COPY target/spring-petclinic-vets-service-4.0.1.jar app.jar

# Vets Service listens on this port.
EXPOSE 8083

ENTRYPOINT ["java", "-jar", "app.jar"]
