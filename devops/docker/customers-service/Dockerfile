# Java runtime used to start the Spring Boot Customers Service.
FROM eclipse-temurin:17

WORKDIR /app

# Copy the JAR produced by `./mvnw clean verify` for this service.
COPY target/spring-petclinic-customers-service-4.0.1.jar app.jar

# Customers Service listens on this port.
EXPOSE 8081

ENTRYPOINT ["java", "-jar", "app.jar"]
