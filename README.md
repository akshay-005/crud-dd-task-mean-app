# MEAN Stack CRUD App - DevOps Assignment

## Project Structure
```
crud-dd-task-mean-app/
├── backend/                 # Node.js + Express API
│   ├── app/
│   │   ├── config/db.config.js
│   │   ├── controllers/tutorial.controller.js
│   │   ├── models/tutorial.model.js
│   │   └── routes/turorial.routes.js
│   ├── Dockerfile
│   ├── package.json
│   └── server.js
├── frontend/                # Angular app
│   ├── src/
│   ├── Dockerfile
│   └── nginx.conf
├── .github/
│   └── workflows/
│       └── docker-ci.yml       # CI/CD pipeline
├── docker-compose.yml
└── README.md
```

## Tech Stack
- **MongoDB** - Database (NoSQL)
- **Express.js** - Backend REST API framework
- **Angular 15** - Frontend framework
- **Node.js** - Backend runtime

## Local Setup

### Prerequisites
- Docker Desktop installed
- Node.js 18+

### Run locally with Docker
```bash
git clone <your-repo-url>
cd crud-dd-task-mean-app
docker compose up --build
```
Visit: http://localhost

## AWS EC2 Deployment

### 1. Launch EC2 Instance
- AMI: Ubuntu Server 24.04 LTS
- Instance type: t3.micro (free tier)
- Security group: Allow ports 22 (SSH), 80 (HTTP), 8080 (API)

### 2. Connect to EC2
```bash
ssh -i your-key.pem ubuntu@YOUR_EC2_IP
```

### 3. Install Docker on EC2
```bash
sudo apt update
sudo apt install -y docker.io docker-compose-plugin
sudo usermod -aG docker ubuntu
newgrp docker
```

### 4. Clone and run
```bash
git clone <your-repo-url>
cd crud-dd-task-mean-app
docker compose up -d --build
```

Visit: http://YOUR_EC2_IP

## CI/CD Pipeline (GitHub Actions)

### GitHub Secrets required:
| Secret | Value |
|--------|-------|
| `DOCKER_USERNAME` | Your Docker Hub username |
| `DOCKER_PASSWORD` | Your Docker Hub password/token |
| `EC2_HOST` | Your EC2 public IP |
| `EC2_SSH_KEY` | Content of your .pem file |

### How it works:
1. Push code to `main` branch
2. GitHub Actions builds Docker images
3. Images pushed to Docker Hub
4. SSH into EC2, pull new images, restart containers