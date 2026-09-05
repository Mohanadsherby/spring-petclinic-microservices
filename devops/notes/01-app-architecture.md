# App architecture — what I'm deploying

The Spring PetClinic app is 9 services in 3 layers. Startup ORDER matters.

## Layer 1 — Infrastructure (start FIRST, in this order)
| Service           | Port | Job |
|-------------------|------|-----|
| config-server     | 8888 | Central configuration. Every other service asks it for settings on boot. |
| discovery-server  | 8761 | Eureka service registry. Services register here so they can find each other. |

## Layer 2 — Business services (depend on Layer 1 being healthy)
| Service           | Port | Job |
|-------------------|------|-----|
| customers-service | 8081 | Owners + pets data |
| visits-service    | 8082 | Vet visit records |
| vets-service      | 8083 | Veterinarians data |
| genai-service     | 8084 | AI chat feature (needs OPENAI_API_KEY — optional) |

## Layer 3 — Entry point + tools
| Service        | Port | Job |
|----------------|------|-----|
| api-gateway    | 8080 | The actual PetClinic website. Routes traffic to the business services. |
| admin-server   | 9090 | Spring Boot Admin UI (optional) |
| tracing-server | 9411 | Zipkin distributed tracing (optional) |

## The golden rule
config-server → discovery-server → business services → api-gateway

On boot, each business service:
1. Calls config-server (8888) for its config
2. Registers itself in discovery-server (8761)

If 8888 and 8761 aren't healthy first, everything else crash-loops.
This dependency ordering is THE central challenge in docker-compose and Kubernetes.

## Tech facts
- Language: Java 17, Spring Boot / Spring Cloud
- Build tool: Maven (./mvnw)
- Each service builds into a runnable .jar in its own target/ folder
