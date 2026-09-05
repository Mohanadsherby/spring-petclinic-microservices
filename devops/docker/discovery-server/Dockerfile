# Java runtime used to start the Spring Boot Discovery Server.
FROM eclipse-temurin:17

WORKDIR /app

# Copy the JAR produced by `./mvnw clean verify` for this service.
COPY target/spring-petclinic-discovery-server-4.0.1.jar app.jar

# Eureka Discovery Server listens on this port.
EXPOSE 8761

ENTRYPOINT ["java", "-jar", "app.jar"]
