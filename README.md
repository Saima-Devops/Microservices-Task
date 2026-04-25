# Microservices Docker Compose Project

### Skill Test 1: Cloud and Containers

---

## Overview

This project showcases a microservices-based architecture built with Node.js, where each service is independently developed, containerized using Docker, and orchestrated via Docker Compose.

The system is designed to demonstrate service separation, container networking, and centralized request routing through a gateway service.

------

## Services and Ports

I was given the following four separate services, each running on its own port:

* User Service → 3000
* Product Service → 3001
* Order Service → 3002
* Gateway Service → 3003

Each service is responsible for handling its own specific functionality.

---

## Architecture

The system follows a gateway-based routing pattern:

```
Client → Gateway Service → (User | Product | Order Services)
```

Instead of calling each service directly, all requests go through the Gateway Service, which then routes them to the appropriate microservice.

---
