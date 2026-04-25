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

### To Remove all containers if they were not gone with compose down

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

<br>

Done!!👍

----
## Author

**Saima Usman**\
Jr. DevOps Engineer\
(PPMCAD-15 HeroVired)

**GitHub:** https://github.com/Saima-Devops

---
