# Microservices Project with Docker Compose + Kubernetes Orchestration 

This project was developed as part of the skill assessment conducted by HeroVired during my PPMCAD learning journey. It consists of a Node.js-based application composed of four independent microservices designed for modular and scalable architecture.

The application was deployed using two different approaches to demonstrate flexibility in deployment strategies and to strengthen practical understanding of containerized environments and orchestration workflows.

Let us explore both approaches individually for a clearer understanding of the deployment process.

1. **Skill Test 1:** [Containerization with Docker & Docker-Compose](https://github.com/Saima-Devops/Microservices-Task/blob/main/README.md#skill-test-1-containerization-with-docker--docker-compose)
2. **Skiltest-2:** [Container Orchestration with Kubernetes](https://github.com/Saima-Devops/Microservices-Task/blob/main/README.md#skiltest-2-container-orchestration-with-kubernetes)

-----

### Skill Test 1: Containerization with Docker & Docker-Compose 

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

## Forked the Repository and Pushed to Github

<img width="1919" height="1077" alt="image" src="https://github.com/user-attachments/assets/c8aab80f-2254-44ce-9036-a88a12066873" />

---

## Running the Application

To run the entire system, I used an Ubuntu EC2 instance to install Docker and Docker Compose:

**1. Updated Packages**
```
sudo apt update && sudo apt upgrade -y
````

**2. Installed Docker**

```
sudo apt install docker.io -y
```

**3. Started and Enabled Docker**

```
sudo systemctl start docker
sudo systemctl enable docker
```

**4. Added Permissions** 

```
sudo usermod -aG docker $USER
exit
```


**5. Reconnected again via ssh**

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/1e572e1f-ca3c-48f9-a93a-0e44467d7fee" />

<br>

**6. Verified Docker**

```
docker --version
```

**7. Installed Docker Compose**

```
# Download Docker Compose Binary
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

# Apply Execute Permissions
sudo chmod +x /usr/local/bin/docker-compose

# Verify Installation
docker-compose --version

```
----

**8. Ran my project on ec2**


```bash
cd Microservices-Task

# Build the Image through docker compose

docker-compose up --build
```

This command builds the Docker images for all services and starts them together in a shared network (bridge network).


<img width="1919" height="1074" alt="image" src="https://github.com/user-attachments/assets/24e5c40a-43d2-4b7b-90a1-90dea2136c7c" />

<img width="1913" height="490" alt="image" src="https://github.com/user-attachments/assets/cb8889c6-e257-4b11-ac31-8f1c0c7d52c7" />


<br>

**Opened all end points on EC2 through security group inbound rules.**

<img width="1919" height="1023" alt="image" src="https://github.com/user-attachments/assets/93f65b9d-5c4c-433a-901f-0abf2adac066" />


-----

## Verifying Containers

To confirm that all containers were running properly, I checked:

```bash
docker ps
```

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/ef62a2ec-c9e9-43c9-9ffa-099408812903" />

<br>

**Checked image:**


```bash
docker images
```

<img width="1896" height="603" alt="image" src="https://github.com/user-attachments/assets/a7390afa-7e1e-4cfe-9a3b-bbebba58c877" />

<br>

**To check custom bridge network whicj created:**


```bash
docker network ls
```

<img width="1887" height="416" alt="image" src="https://github.com/user-attachments/assets/a5335bf5-6a0a-4f98-90b0-ef0017f20bd1" />


---

## Service Endpoints

Once everything was running, I accessed the services using these endpoints:

* http://ec2-ip:3000/users
* http://ec2-ip:3001/products
* http://ec2-ip:3002/orders
* http://ec2-ip:3003/health

---

## Testing

### Browser

I tested the services by opening the endpoints in a browser to make sure each one responded correctly.

<br>

* http://ec2-ip:3000/users
  
<img width="1918" height="1079" alt="image" src="https://github.com/user-attachments/assets/2ac2e0b1-c1da-4b98-aa7b-86212de49a81" />

<br>

* http://ec2-ip:3001/products

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/20706e4f-becb-4e2e-b448-219180b20ecd" />

<br>

* http://ec2-ip:3002/orders

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/457cb66f-191c-48f1-b5b2-8fbe835fba8a" />

<br>

* http://ec2-ip:3003/health

<img width="1914" height="1075" alt="image" src="https://github.com/user-attachments/assets/42a3b552-778f-4f1d-bfc2-8ce36df2f960" />

---

### cURL

I also used cURL to test from the command line:

```bash id="curl1"
curl http://localhost:3000/users
curl http://localhost:3001/products
curl http://localhost:3002/orders
curl http://localhost:3003/health
```

<img width="1919" height="1022" alt="image" src="https://github.com/user-attachments/assets/b5552b89-6459-4660-a686-cae0cb034536" />


---

## Docker Setup Real Magic

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

----

## Clean Up After Project

### To Stop Containers:

```
docker-compose down
```
<img width="1917" height="496" alt="image" src="https://github.com/user-attachments/assets/b6714521-a352-414a-a3ce-e20b21fc57ad" />

<br>

### To remove all containers if they were not gone with compose down

```
docker rm -f $(docker ps -aq)
```


<br>

### To Remove images

```
docker rmi -f $(docker images -aq)
```

<img width="1908" height="446" alt="image" src="https://github.com/user-attachments/assets/37e7a358-2033-4e64-ab1f-2eab0b56da60" />


<br>

### To Remove unused data

```
docker system prune -a -f
```

<img width="958" height="762" alt="image" src="https://github.com/user-attachments/assets/1b143c95-15de-434e-a5e3-a49d95a23d8c" />

<br>

### Remove the custom network if not gone with compose down

```
docker network rm node-app-network
```

<img width="1919" height="608" alt="image" src="https://github.com/user-attachments/assets/93aaa67c-413d-42df-86c5-7c8fa2c2dbc6" />


<br>

### To Delete project folder

```
cd ~
rm -rf Microservces-Task
```

<img width="1909" height="651" alt="image" src="https://github.com/user-attachments/assets/4371fe6a-dbe6-4e3e-be40-d7b7036cda8d" />

----

**Part-01 Done!** 👍

----

# Skiltest-2 Container Orchestration with Kubernetes

This part focuses on Kubernetes deployments, service configuration, container orchestration, service discovery, and validation of inter-service communication using Minikube.

------

## Project Objectives

The primary objectives of this project are to:

- Deploy multiple **Node.js–based microservices** within a `Kubernetes` environment
- Configure and manage Kubernetes `Deployments` and `Services` effectively
- Establish reliable inter-service communication within the `Kubernetes cluster`
- Utilize `Minikube` as the local Kubernetes development and testing platform
- Verify application availability, service accessibility, and `pod` health status
- Gain practical understanding of container `orchestration` and Kubernetes-based application management using Kubernetes

-------

# App Components & 4 Microservices

The application consists of four containerized Node.js microservices:

| Service Name | Description | Port |
|---|---|---|
| User Service | Handles user-related operations | 3000 |
| Product Service | Handles product-related operations | 3001 |
| Order Service | Handles order-related operations | 3002 |
| Gateway Service | Acts as API gateway and entry point | 3003 |

The Gateway Service acts as the primary entry point to the application, handling external client requests and routing them to the appropriate internal services within the system.

----

## Project Heirarchy

```
submission/
│
├── README.md
│
├── deployments/
│   ├── user-service.yaml
│   ├── product-service.yaml
│   ├── order-service.yaml
│   └── gateway-service.yaml
│
├── services/
│   ├── user-service.yaml
│   ├── product-service.yaml
│   ├── order-service.yaml
│   └── gateway-service.yaml
│
├── ingress/                     
│   └── ingress.yaml
│
├── screenshots/ (All captured shots are here)
│  
├── user-service-source-code/
│   ├── Dockerfile
│   ├── package.json
│   ├── package-lock.json
│   
├── product-service-source-code/
│   ├── Dockerfile
│   ├── package.json
│   ├── package-lock.json
│   
├── order-service-source-code/
│   ├── Dockerfile
│   ├── package.json
│   ├── package-lock.json
│   
└── gateway-service-source-code/
    ├── Dockerfile
    ├── package.json
    ├── package-lock.json
```
------

## Technologies and Tools Utilized

The following technologies and development tools were utilized throughout the implementation of this project:

- Node.js
- Docker Desktop
- Kubernetes
- Minikube
- kubectl
- Visual Studio Code
-  Git and GitHub

-----

## Kubernetes Resources Configuration

### Deployments

Dedicated Kubernetes Deployment manifests were created and configured for each of the four microservices within the application architecture.

Each deployment definition includes:

- Container image specifications
- Labels and selector configurations
- Resource requests and limit settings
- Environment variable definitions
- Replica management configuration
- Liveness and readiness probe settings 

These deployments provide automated pod orchestration, scalability, self-healing capabilities, and high availability within the Kubernetes cluster.

---

### Services

Kubernetes Services were implemented for all microservices to enable secure and reliable communication between components inside the cluster.

### Service Types Used in this Project

| Service | Type |
|---|---|
| User Service | ClusterIP |
| Product Service | ClusterIP |
| Order Service | ClusterIP |
| Gateway Service | NodePort |

`ClusterIP` services provide internal communication between services, while the Gateway Service uses `NodePort` to allow external access from the browser.

-----

### Minikube Configuration

**Minikube** was utilized as the local Kubernetes environment for deploying, managing, and testing the application.

The **Docker Desktop** driver was configured with Minikube to streamline container execution and simplify the local deployment workflow.

The **Kubernetes cluster** was successfully initialized, and all **Deployment** and **Service** configurations were applied and managed using **kubectl**.

-----

## Application Deployment Process

The application deployment procedure was carried out through the following stages:

1. Building and containerizing all microservices using Docker images
2. Initializing the Minikube cluster environment
3. Deploying the Kubernetes Deployment manifests
4. Configuring and applying Kubernetes Service manifests
5. Validating pod health, deployment status, and service configurations
6. Testing application availability and external access through the Gateway Service

All Kubernetes resources were successfully deployed, configured, and verified using kubectl commands.

----


## Step 1 — Verification 

```
docker --version
kubectl version --client
minikube version
```

**Everything is UP & RUNNING!**

---

## Step 2 — Started Minikube

```
minikube start

#Verify:
kubectl get nodes
```

<img width="2142" height="994" alt="image" src="https://github.com/user-attachments/assets/4aac8a37-6e0c-4d84-8fe1-ca031bd2d9b4" />

---

## Step 3 — Enabled Ingress

```
minikube addons enable ingress

#Verify:
kubectl get pods -n ingress-nginx
```

<img width="2560" height="1600" alt="image" src="https://github.com/user-attachments/assets/7f69c4b4-3496-4e44-bc5e-04eb0779317a" />

<img width="2560" height="1600" alt="image" src="https://github.com/user-attachments/assets/d53de946-e758-4203-b498-6f2128e7f8ed" />

<img width="1678" height="624" alt="image" src="https://github.com/user-attachments/assets/fe6a47af-58a5-4b5b-b833-2d06fb74eac5" />


----

## Step 4 — Loaded Docker Images into Minikube

```
docker images
```

```
minikube image load user-service:latest
minikube image load product-service:latest
minikube image load order-service:latest
minikube image load gateway-service:latest

#Verify:
minikube image ls
```

<img width="2560" height="1600" alt="image" src="https://github.com/user-attachments/assets/b1e2e820-240a-46b6-941d-c755926d378e" />

----

## Step 5 — Created Deployment YAML Files 

```
nano submission/deployments/user-service.yaml
nano submission/deployments/product-service.yaml
nano submission/deployments/order-service.yaml
nano submission/deployments/gateway-service.yaml
```

-----

## Step 6 — Created Service YAML Files 

```
nano submission/services/user-service.yaml
nano submission/services/product-service.yaml
nano submission/services/order-service.yaml
nano submission/services/gateway-service.yaml
```
---

## Step 6 — Deployed Everything

**Applied Deployments**

```
kubectl apply -f deployments/
```

**Applied Services**
```
kubectl apply -f services/
```


<img width="2560" height="1600" alt="image" src="https://github.com/user-attachments/assets/0742eaed-9126-4696-a8b1-42fd49049d22" />

<img width="2560" height="1600" alt="image" src="https://github.com/user-attachments/assets/911d0b46-0424-466b-9cd2-9ce9e0d61b66" />

----

## Step 7 — Verified Everything

### Pods:

```
kubectl get pods
```

### Services:

```
kubectl get svc
```

### Deployments:

```
kubectl get deployments
```

### Checked Logs

```
kubectl logs deployment/gateway-service
````

<img width="2560" height="1600" alt="image" src="https://github.com/user-attachments/assets/00b676fd-8bce-47ec-8693-130d904e8849" />


----

## Step 8 — Tested the Application

```
kubectl port-forward svc/gateway-service 3003:3003
```

**in Browser:**

```
http://localhost:3003
```

**Tested APIs**

```
curl http://localhost:3003/api/users
curl http://localhost:3003/api/products
curl http://localhost:3003/api/orders
```

<img width="2560" height="1600" alt="image" src="https://github.com/user-attachments/assets/cefc54d9-c3d8-41f7-8f73-70434744b3fb" />

<img width="2560" height="1600" alt="image" src="https://github.com/user-attachments/assets/706e0a07-cc6d-4bad-a84c-2beba2c46037" />

<img width="2560" height="1600" alt="image" src="https://github.com/user-attachments/assets/6200b10e-17e4-4a18-9ab7-92427e7efee7" />


---

**Done!!** 👍

---

## Conclusion

This project effectively demonstrates the deployment and orchestration of a microservices-based Node.js application using Kubernetes and Minikube.

All services were successfully containerized, deployed, exposed, and validated within the Kubernetes cluster environment. This implementation provides practical exposure to Kubernetes architecture, deployment strategies, inter-service communication, and local cluster management using Minikube.

----

## Author

**Saima Usman**\
Jr. DevOps Engineer\
(PPMCAD-15 HeroVired)

**GitHub:** https://github.com/Saima-Devops

---

