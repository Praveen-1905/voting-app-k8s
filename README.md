Docker Voting Application
A distributed voting setup built with microservices. It uses containerization with Docker and can run on Kubernetes.

🎯 Overview
This app runs across several small services that work together. Users can cast a vote between two choices, and the results update in real time on a separate webpage.

🏗️ Architecture
The system includes five parts:

* Vote service written in Python Flask
* Redis for temporary storage
* Worker service that moves the votes from Redis to PostgreSQL
* PostgreSQL for permanent storage
* Result service written in Python Flask for showing the vote counts

Technology Stack
Vote frontend: Python 3.9 with Flask
Result frontend: Python 3.9 with Flask
Worker: Python 3.9
Message queue: Redis
Database: PostgreSQL 15 Alpine
Containerization: Docker and Docker Compose
Orchestration: Kubernetes

📊 Data Flow
User Vote → Vote Service → Redis → Worker → PostgreSQL → Result Service → User View

🚀 Quick Start

Prerequisites
Docker, Docker Compose, Kubernetes cluster, Docker Hub account

Running with Docker Compose
Clone the repo:

```
git clone https://github.com/denish952/docker-voting-app.git
cd docker-voting-app
```

Start the services:

```
docker-compose up --build -d
```

Access the frontends:
Vote app: [http://localhost:5000](http://localhost:5000)
Result app: [http://localhost:5001](http://localhost:5001)

Stop the stack:

```
docker-compose down
```

Running on Kubernetes
Move to the manifests:

```
cd k8s-manifests
```

Apply the deployments:

```
kubectl apply -f .
```

Check the status:

```
kubectl get pods
kubectl get services
```

Access on NodePort:
Vote: http://<node-ip>:30000
Result: http://<node-ip>:30001

Minikube users can run:

```
minikube service vote
minikube service result
```

📦 Docker Images
Images pushed to Docker Hub:

praveenkumar2204/voting-app-vote:v1
praveenkumar2204/voting-app-result:v1
praveenkumar2204/voting-app-worker:v1

Build and push:

```
docker-compose build

docker tag docker-voting-app-vote denish952/voting-app-vote:v1
docker tag docker-voting-app-result denish952/voting-app-result:v1
docker tag docker-voting-app-worker denish952/voting-app-worker:v1

docker push denish952/voting-app-vote:v1
docker push denish952/voting-app-result:v1
docker push denish952/voting-app-worker:v1
```

📁 Project Layout
```
docker-voting-app/
├── vote/
│   ├── app.py
│   ├── requirements.txt
│   └── Dockerfile
├── result/
│   ├── app.py
│   ├── requirements.txt
│   └── Dockerfile
├── worker/
│   ├── worker.py
│   ├── requirements.txt
│   └── Dockerfile
├── k8s-yaml/
│   ├── vote-deployment.yaml
│   ├── result-deployment.yaml
│   ├── worker-deployment.yaml
│   ├── redis-deployment.yaml
│   └── db-deployment.yaml
├── docs/
│   ├── architecture-diagram.png
│   ├── docker-architecture.png
│   └── kubernetes-architecture.png
├── docker-compose.yml
└── README.md
```
🔧 Configuration

Environment Variables
Vote service:
REDIS_HOST

Worker service:
REDIS_HOST
POSTGRES_HOST
POSTGRES_USER
POSTGRES_PASSWORD

Result service:
POSTGRES_HOST
POSTGRES_USER
POSTGRES_PASSWORD

Port Mapping
Docker Compose:
Vote → 5000:80
Result → 5001:80

Kubernetes:
Vote → NodePort 30000
Result → NodePort 30001

🎓 What You Learn
How microservices interact
How to containerize applications
How to deploy and manage services on Kubernetes
How to manage state using Redis and PostgreSQL
How background jobs work
How to structure a project that can easily fit into CI/CD pipelines

🐛 Troubleshooting

Docker Compose

```
docker compose logs vote
docker compose logs worker
docker compose logs result
docker compose restart
```

Kubernetes

```
kubectl get pods
kubectl describe pod <pod-name>
kubectl logs <pod-name>
kubectl logs -f deployment/worker
kubectl delete -f k8s-manifests/
kubectl apply -f k8s-manifests/
```

🤝 Contributing
Feel free to fork the repo and open a pull request.

👤 Author
PraveenKumar
```
Docker Hub: praveenkumar2204
GitHub: Praveen-1905
```
