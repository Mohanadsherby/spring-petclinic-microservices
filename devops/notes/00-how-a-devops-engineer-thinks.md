# How a DevOps engineer thinks

The most valuable skill is the thought process, not the commands. When handed a
new app, don't touch any tool yet. Ask questions IN ORDER — each answer unlocks
the next decision.

## The questions, in order

### Q1 — "What is this thing?"
Before anything: what am I even deploying?
- One app or many?      → 8 microservices, not one app
- What language/runtime? → Java 17, Spring Boot
- How does it build?     → Maven (`./mvnw`)

Why: it decides every tool downstream. Java means a JDK in the images.
Microservices means orchestrating many containers, not running one.

### Q2 — "What are the moving parts, and how do they depend on each other?"
Which pieces must exist, and in what order?
- config-server + discovery-server start FIRST. Everyone else depends on them.

Why: dependencies decide startup order, health checks, and networking.
Get it wrong and everything crash-loops. (This is why we drew the 3-layer
diagram before writing any Dockerfile.)

### Q3 — "How do I run ONE piece by hand?"
Can I build and run a single service manually?
- Compile to a .jar, run it.

Why: YOU CANNOT AUTOMATE WHAT YOU CAN'T DO MANUALLY. Automation is just
"record the manual steps, then make a robot repeat them." Always do it by
hand once, first.

### Q4 — "How do I package it so it runs anywhere?"
- Docker image.

Why: "works on my machine" is the enemy. A container runs identically everywhere.

### Q5 — "How do I run all the pieces together?"
- docker-compose locally, then Kubernetes.

### Q6 — "How do I make this repeatable and automatic?"
- CI/CD pipeline (build -> test -> scan -> deploy on every code change).

### Q7 — "How do I know it's healthy in production?"
- Monitoring, logs, alerts (Prometheus / Grafana).

### Q8 — "What happens when it breaks?"
- Chaos testing, resilience, rollback.

## The pattern behind all of it

    Understand  ->  Do it manually once  ->  Package it  ->
    Automate the packaging  ->  Watch it  ->  Harden it

Every phase in the roadmap is just one of these questions. Each tool is an
answer to a question:
- Docker            answers Q4
- docker-compose    answers Q5
- GitHub Actions    answers Q6
- Prometheus        answers Q7

## The one habit that matters most
Before touching any tool, ask:
"What problem does this solve, and could I do it by hand first?"
If you can't explain the problem, you're not ready for the tool.
That single habit separates engineers from people who copy-paste commands.
