# Attack & Defense Challenge Setup

This document provides instructions on setting up an attack and defense challenge using Docker and specific tools like the attacker/submitter from [S4DFarm](https://github.com/C4T-BuT-S4D/S4DFarm).

## 1. Essential Docker Commands

Here are some fundamental commands to manage Docker containers:

### Starting and Managing Containers
```bash
# Run a container in the background
docker run -d --name container_name image

# Stop a container
docker stop container_name

# Start a stopped container
docker start container_name

# Restart a container
docker restart container_name

# Remove a container
docker rm container_name
```

### Managing Images
```bash
# Download an image from Docker Hub
docker pull image_name

# Build an image from a Dockerfile
docker build -t image_name .

# List local images
docker images

# Remove an image
docker rmi image_name
```

### Monitoring and Debugging
```bash
# Access a running container
docker exec -it container_name /bin/sh

# View container logs
docker logs container_name

# List active containers
docker ps

# List all containers (including stopped ones)
docker ps -a
```

## 2. Using Attacker/Submitter (S4DFarm)

### Installation
```bash
git clone https://github.com/C4T-BuT-S4D/S4DFarm.git
cd S4DFarm
docker compose up --build -d
```

### Configuration
Modify the configuration file to define competition details and endpoints.

### Running an Attack
```bash
python3 attacker.py --team TEAM_NAME --ip TARGET_IP
```

### Submitting a Flag
```bash
python3 submitter.py --team TEAM_NAME --flag FLAG_VALUE
```

## 3. Analyzer (to be completed)

## 4. Proxy (to be completed)
