# Attack & Defense Challenge Setup

This document provides instructions on setting up an attack and defense challenge using Docker and specific tools like the attacker/submitter from [S4DFarm](https://github.com/C4T-BuT-S4D/S4DFarm), the proxy [Firegex](https://github.com/Pwnzer0tt1/firegex.git)  and the analyzer [Tulip](https://github.com/OpenAttackDefenseTools/tulip.git).

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

## 2. Attacker/Submitter (S4DFarm)
DEFAULT PORT: 5137

### Installation
```bash
git clone https://github.com/C4T-BuT-S4D/S4DFarm.git
cd S4DFarm
# FIX: RUN corepack use pnpm@8.x 
code server/docker/front/Dockerfile
```

### Configuration
Modify the configuration file to define competition details and endpoints.
```bash
# Define competition details and endpoints
# 'SYSTEM_PROTOCOL': 'your_prot',
# 'SYSTEM_HOST': 'submit_ip',
# 'SYSTEM_PORT': 'submit_port',
# 'TEAM_TOKEN': 'your_team_token',
code server/app/config.py

# Make a protocol
cd server/app/protocols
cp volgactf.py ctf_prot.py
code ctf_prot.py
cd ../../../
```

**Note:** Remember to change the password in both `compose.yaml` and `config.py` to ensure proper configuration and security.

### Usage
```bash
docker compose up --build -d
```

### Running an Attack
```bash
cd client
# FARM-IP default: localhost:5137
scp psw.py root@91.99.54.223:../home/schiavo/S4DFarm/client/
python3 start_sploit.py --server-url http://FARM-IP/ --server-pass YOUR_PASS exploit.py
```
**Note:** Two important elements that should be included in your exploit script are: `#!/usr/bin/env python3` to specify the correct Python interpreter, and `print(flag, flush=True)` to ensure the flag is printed correctly by forcing the buffer to flush.

## 3. Analyzer (Tulip)
DEFAULT PORT: 3000

### Installation
```bash
git clone https://github.com/OpenAttackDefenseTools/tulip.git
```

### Configuration
```bash
cd tulip
cp .env.example .env

# set up
code .env.example

# Edit properly
# TRAFFIC_DIR_HOST="./services/test_pcap, to redirect .pcap
code services/configurations.py
```

### Usage
```bash
docker-compose up -d --build
```

## 4. Proxy (Firegex)
DEFAULT PORT: 4444

### Installation
```bash
git clone https://github.com/Pwnzer0tt1/firegex.git
cd firegex
python3 start.py
```

## Some useful command
* `scp -i ~/.ssh/yourkey -r ./proxy masamune@IP:/tmp/source` Copy resource from your local to your vulnbox.
* `passwd` Change your password.
* `ssh-keygen -t ed25519` Generating an ssh public key and private key pair.
