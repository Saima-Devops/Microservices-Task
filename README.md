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

## Project Structure

I organized the project as follows:

```
skilltest1/
├── submissions/
│   ├── user-service/
│   ├── product-service/
│   ├── order-service/
│   ├── gateway-service/
├── docker-compose.yml
├── README.md
└── .gitignore
```

Each service is placed in its own folder to keep the code modular and easy to manage.

---

## Technology Stack

* Node.js
* Express.js
* Docker
* Docker Compose

---

## Getting Started

### Prerequisites

Before running the project, I made sure Docker and Docker Compose were installed on my system. I verified this using:

```bash 
docker --version
docker-compose --version
```

---

## Running the Application

To run the entire system, I used:

```bash
docker-compose up --build
```

This command builds the Docker images for all services and starts them together in a shared network (bridge network).

---

## Verifying Containers

To confirm that all containers were running properly, I checked:

```bash
docker ps
```

---

## Service Endpoints

Once everything was running, I accessed the services using these endpoints:

* http://localhost:3000/users
* http://localhost:3001/products
* http://localhost:3002/orders
* http://localhost:3003/health

---

## Testing

### Browser

I tested the services by opening the endpoints in a browser to make sure each one responded correctly.

---

### cURL

I also used cURL to test from the command line:

```bash id="curl1"
curl http://localhost:3000/users
curl http://localhost:3001/products
curl http://localhost:3002/orders
curl http://localhost:3003/health
```

---

## Docker Setup

### Dockerfile

For each service, I created a Dockerfile where I:

* Used a Node.js base image
* Installed dependencies
* Exposed the required port
* Ran the app using `node app.js`

---

### docker-compose.yml

In the docker-compose file, I:

* Defined all four services in a single YAML file
* Configured them to run together
* Creates a shared bridge network for inter-service communication
* Manages container startup order and dependencies

---

## Troubleshooting

### Port Issues

Port Already in Use

```bash
lsof -i :3000
kill -9 <PID>
```

---

### Logs

To debug issues, I checked logs using:

```bash id="logs1"
docker-compose logs
```

---

### Rebuilding

If something didn’t work, I restarted everything with:

```bash
docker-compose down
docker-compose up --build
```

---

## Future Improvements

If I were to extend this project, I would:

* Improve the API Gateway routing
* Implement logging and monitoring
* Explore scaling the services

---
## Submission

The project is fully containerized using Docker and orchestrated using Docker Compose to simulate a microservices architecture.

✅ Final Checklist Before Submission

✔ All Dockerfiles included\
✔ docker-compose.yml included\
✔ README.md complete\
✔ No node_modules\
✔ ZIP created correctly

----

## Author

**Saima Usman**\
Jr. DevOps Engineer\
(PPMCAD-15 HeroVired)

**GitHub:** https://github.com/Saima-Devops

---
