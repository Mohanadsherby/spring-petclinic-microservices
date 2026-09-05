# Java runtime used to start the Spring Boot API Gateway.
FROM eclipse-temurin:17

WORKDIR /app

# Copy the JAR produced by `./mvnw clean verify` for this service.
COPY target/spring-petclinic-api-gateway-4.0.1.jar app.jar

# API Gateway listens on this port and is the public application entry point.
EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]
