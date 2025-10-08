# Docker + Kubernetes Node.js App

## Project Overview
This project demonstrates how to containerize a Node.js application using **Docker** and deploy it on a local **Kubernetes cluster** (Minikube). It includes:

- A simple Node.js Express app.
- Dockerfile to build the Docker image.
- Kubernetes Deployment and Service manifests.
- Instructions to run locally using Docker and Minikube.

---

## Prerequisites
Make sure you have installed:

- [Node.js](https://nodejs.org/)
- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- [Minikube](https://minikube.sigs.k8s.io/docs/)

---

## Project Structure

docker-k8s-app/
├─ app.js # Node.js Express app
├─ package.json # Project dependencies
├─ Dockerfile # Docker image build instructions
├─ kubernetes/
│ ├─ deployment.yaml # Kubernetes Deployment manifest
│ └─ service.yaml # Kubernetes Service manifest
└─ README.md # Project documentation

yaml
Copy code

---

## Node.js Application

A simple Express server running on **port 3000**:

```js
const express = require('express');
const app = express();
const PORT = 3000;

app.get('/', (req, res) => {
  res.send('Hello from Docker + Kubernetes Node.js App!');
});

app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});
Docker
Build Docker Image
bash
Copy code
docker build -t my-docker-k8s-app .
Run Docker Container
bash
Copy code
docker run -d -p 3000:3000 my-docker-k8s-app
Check the app in your browser: http://localhost:3000

Kubernetes (Minikube)
1. Start Minikube
bash
Copy code
minikube start
2. Deploy the Application
bash
Copy code
kubectl apply -f kubernetes/deployment.yaml
kubectl apply -f kubernetes/service.yaml
3. Check Pods and Services
bash
Copy code
kubectl get pods
kubectl get svc
4. Access the Service
bash
Copy code
minikube service docker-k8s-app-service
This will open your default browser with the Node.js app running through the Kubernetes Service.

Notes
Make sure to tag and push your Docker image to Docker Hub if using a remote Kubernetes cluster:

bash
Copy code
docker tag my-docker-k8s-app <dockerhub-username>/my-docker-k8s-app:latest
docker push <dockerhub-username>/my-docker-k8s-app:latest
In deployment.yaml, update image: with your Docker Hub repository if needed.
