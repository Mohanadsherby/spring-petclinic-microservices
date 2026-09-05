# Java runtime used to start the Spring Boot GenAI Service.
FROM eclipse-temurin:17

WORKDIR /app

# Copy the JAR produced by `./mvnw clean verify` for this service.
COPY target/spring-petclinic-genai-service-4.0.1.jar app.jar

# GenAI Service listens on this port.
EXPOSE 8084

ENTRYPOINT ["java", "-jar", "app.jar"]
