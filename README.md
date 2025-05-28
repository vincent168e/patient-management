# Patient Management System (Backend)

This project demonstrates a patient management system using a Spring Boot-based microservices architecture. It comprises five modules: patient-service, analytics-service, api-gateway, auth-service, and billing-service, built with Spring Boot 3.4.5 and Java 21. The patient-service manages patient data using Spring Data JPA and PostgreSQL, organized under src/main/java/com/pm/patientservice with a Patient entity and REST endpoints. The billing-service connects to patient-service via gRPC for synchronous communication, while the analytics-service integrates with patient-service through Kafka for event-driven data processing. The auth-service implements JWT-based authentication, securing API access. The api-gateway routes requests to respective services. Each module includes internal API request handling and integration test scripts for validation. A parent pom.xml manages shared dependencies, and Dockerfiles enable containerization. This modular setup ensures scalable, independent microservices with robust communication and testing.

# Api Gateway

---

## Environment Variables
```
AUTH_SERVICE_URL=http://auth-service:4005
```

## Bind Ports
```
4004:4004
```

# Patient Service

---

## Environment Variables
```
BILLING_SERVICE_ADDRESS=billing-service
BILLING_SERVICE_GRPC_PORT=9005
JAVA_TOOL_OPTIONS=-agentlib:jdwp\=transport\=dt_socket,server\=y,suspend\=n,address\=*:5005
SPRING_DATASOURCE_PASSWORD=password
SPRING_DATASOURCE_URL=jdbc:postgresql://patient-service-db:5432/db
SPRING_DATASOURCE_USERNAME=admin_user
SPRING_JPA_HIBERNATE_DDL_AUTO=update
SPRING_KAFKA_BOOTSTRAP_SERVERS=kafka:9092
SPRING_SQL_INIT_MODE=always
```

# Analytics Service

---

## Environment Vars

```
SPRING_KAFKA_BOOTSTRAP_SERVERS=kafka:9092
```

## Bind Ports
```
4002:4002
```

# Kafka (Analytics Service)

---

## Environment Variables
```
KAFKA_CFG_ADVERTISED_LISTENERS=PLAINTEXT://kafka:9092,EXTERNAL://localhost:9094
KAFKA_CFG_CONTROLLER_LISTENER_NAMES=CONTROLLER
KAFKA_CFG_CONTROLLER_QUORUM_VOTERS=0@kafka:9093
KAFKA_CFG_LISTENER_SECURITY_PROTOCOL_MAP=CONTROLLER:PLAINTEXT,EXTERNAL:PLAINTEXT,PLAINTEXT:PLAINTEXT
KAFKA_CFG_LISTENERS=PLAINTEXT://:9092,CONTROLLER://:9093,EXTERNAL://:9094
KAFKA_CFG_NODE_ID=0
KAFKA_CFG_PROCESS_ROLES=controller,broker
```

## Bind Ports
```
9092:9092 9094:9094
```

# Auth service

---

## Environment Variables
```
SPRING_DATASOURCE_PASSWORD=password
SPRING_DATASOURCE_URL=jdbc:postgresql://auth-service-db:5432/db
SPRING_DATASOURCE_USERNAME=admin_user
SPRING_JPA_HIBERNATE_DDL_AUTO=update
SPRING_SQL_INIT_MODE=always
```

# Patient Service DB

---

## Environment Variables
```
POSTGRES_DB=db
POSTGRES_PASSWORD=password
POSTGRES_USER=admin_user
```

## Bind Ports
```
5000:5432
```

# Auth Service DB

---

## Environment Variables
```
POSTGRES_DB=db
POSTGRES_PASSWORD=password
POSTGRES_USER=admin_user
```

## Bind Ports
```
5001:5432
```

# Billing Service

---

## Bind Ports
```
4001:4001 9001:9001
```
