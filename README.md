# Three-Tier Chat Application Using Kubernetes

A real-time, containerized chat application built with the **MERN stack**, designed using a three-tier architecture and deployed using **Docker and Kubernetes**.

The application provides real-time messaging, JWT-based authentication, online/offline presence, and profile management. The architecture separates the presentation, application, and database layers to improve scalability, maintainability, and deployment flexibility.

---

## 📌 Project Overview

This project demonstrates how a modern full-stack application can be containerized and deployed using a **three-tier architecture**.

The application is divided into:

1. **Presentation Tier** – React frontend served through Nginx
2. **Application Tier** – Node.js/Express backend with Socket.io
3. **Data Tier** – MongoDB database

Docker is used to containerize the application components, while Kubernetes is used for container orchestration, service discovery, networking, and deployment management.

---

## 🏗️ Architecture

![Application Architecture](https://github.com/user-attachments/assets/f845a188-8e70-42f7-8577-30af38e83053)

```text
                         ┌──────────────────────┐
                         │        Users         │
                         │      Web Browser     │
                         └──────────┬───────────┘
                                    │
                                    │ HTTP / WebSocket
                                    ▼
                         ┌──────────────────────┐
                         │      Frontend        │
                         │    React + Nginx     │
                         │      Port: 80        │
                         └──────────┬───────────┘
                                    │
                                    │ REST API
                                    │ WebSocket
                                    ▼
                         ┌──────────────────────┐
                         │       Backend        │
                         │ Node.js + Express.js │
                         │      Socket.io       │
                         │      Port: 5001      │
                         └──────────┬───────────┘
                                    │
                                    │ MongoDB Protocol
                                    ▼
                         ┌──────────────────────┐
                         │       MongoDB        │
                         │      Port: 27017     │
                         └──────────────────────┘
```

---

# ✨ Features

* 💬 **Real-Time Messaging** using Socket.io
* 🔐 **JWT Authentication & Authorization**
* 👤 **User Profile Management**
* 🟢 **Real-Time Online/Offline Status**
* ⚡ **RESTful APIs**
* 🔄 **WebSocket Communication**
* 🎨 **Modern React UI**
* 📦 **Dockerized Application**
* ☸️ **Kubernetes-Based Deployment**
* 🌐 **Nginx Web Server**
* 🗄️ **MongoDB Persistent Storage**
* 📈 **Scalable Three-Tier Architecture**

---

# 🛠️ Technology Stack

### Frontend

* React.js
* TailwindCSS
* DaisyUI
* Zustand
* Nginx

### Backend

* Node.js
* Express.js
* Socket.io
* JWT
* REST API

### Database

* MongoDB

### DevOps & Infrastructure

* Docker
* Docker Compose
* Kubernetes
* Nginx
* Kubernetes Services
* Kubernetes Deployments
* Kubernetes Namespaces
* Persistent Storage

---

# 📂 Project Structure

```text
Three-Tier-Chat-Application-using-Kubernetes/
│
├── frontend/
│   ├── public/
│   ├── src/
│   ├── Dockerfile
│   └── package.json
│
├── backend/
│   ├── src/
│   ├── Dockerfile
│   ├── .env
│   └── package.json
│
├── k8s/
│   ├── namespace.yaml
│   ├── frontend-deployment.yaml
│   ├── frontend-service.yaml
│   ├── backend-deployment.yaml
│   ├── backend-service.yaml
│   ├── mongodb-deployment.yaml
│   ├── mongodb-service.yaml
│   └── ...
│
├── docker-compose.yml
└── README.md
```

---

# 🔄 Application Workflow

## 1. User Interaction

Users access the application through a web browser.

The React frontend is responsible for:

* User login and registration
* Displaying conversations
* Sending and receiving messages
* Managing user profiles
* Displaying online/offline status
* Handling real-time UI updates

The frontend communicates with the backend using:

* HTTP requests for REST APIs
* WebSocket connections through Socket.io for real-time communication

---

## 2. Backend Processing

The Node.js/Express backend handles the application's business logic.

Responsibilities include:

* User authentication
* JWT token validation
* User management
* Message creation and retrieval
* Database operations
* REST API processing
* WebSocket connections
* Online/offline status management

Socket.io provides bi-directional communication between the frontend and backend.

For example:

```text
User A
   │
   │ Send Message
   ▼
Frontend
   │
   │ WebSocket
   ▼
Backend / Socket.io
   │
   ├──────────────► MongoDB
   │
   ▼
User B
```

This allows messages to be delivered in real time without requiring the browser to continuously refresh the page.

---

## 3. MongoDB Database

MongoDB is responsible for storing persistent application data.

Examples include:

* User information
* Authentication-related data
* Chat messages
* Profile information
* Other application data

The backend communicates with MongoDB to perform:

```text
Create
Read
Update
Delete
```

operations.

---

# 🐳 Docker Containerization

Each application component is containerized independently.

```text
┌─────────────────────────────────────┐
│            Docker Environment       │
│                                     │
│  ┌────────────┐                     │
│  │  Frontend  │                     │
│  │ React/Nginx│                     │
│  └─────┬──────┘                     │
│        │                             │
│        ▼                             │
│  ┌────────────┐                     │
│  │  Backend   │                     │
│  │ Node/Express│                    │
│  └─────┬──────┘                     │
│        │                             │
│        ▼                             │
│  ┌────────────┐                     │
│  │  MongoDB   │                     │
│  └────────────┘                     │
│                                     │
└─────────────────────────────────────┘
```

---

# 🔧 Environment Configuration

Create a `.env` file inside the `backend` directory:

```env
MONGODB_URI=mongodb://mongoadmin:secret@mongodb:27017/dbname?authSource=admin
JWT_SECRET=your_jwt_secret_key
PORT=5001
```

### Environment Variables

| Variable      | Description                            |
| ------------- | -------------------------------------- |
| `MONGODB_URI` | MongoDB connection string              |
| `JWT_SECRET`  | Secret key used for JWT authentication |
| `PORT`        | Backend application port               |

> **Security:** Do not commit `.env` files or real secrets to GitHub. Use Kubernetes Secrets or another secure secret-management solution for production deployments.

---

# 🚀 Local Deployment Using Docker Compose

Docker Compose can be used to run the application locally before deploying it to Kubernetes.

## 1. Clone the Repository

```bash
git clone https://github.com/iemafzalhassan/full-stack_chatApp.git
```

Navigate to the project:

```bash
cd full-stack_chatApp
```

---

## 2. Build and Start the Containers

```bash
docker-compose up -d --build
```

This command:

* Builds the frontend image
* Builds the backend image
* Pulls the MongoDB image
* Creates the required containers
* Starts the application services

---

## 3. Verify Containers

```bash
docker ps
```

Check application logs:

```bash
docker-compose logs -f
```

---

## 4. Access the Application

Open your browser:

```text
http://localhost
```

Backend API:

```text
http://localhost:5001
```

---

# 🐳 Manual Docker Deployment

The application can also be deployed manually without Docker Compose.

## Create Docker Network

```bash
docker network create full-stack
```

---

## Build Frontend Image

```bash
cd frontend
```

```bash
docker build -t full-stack_frontend .
```

---

## Run Frontend Container

```bash
docker run -d \
  --network=full-stack \
  -p 5173:5173 \
  --name frontend \
  full-stack_frontend:latest
```

---

## Run MongoDB

```bash
docker run -d \
  -p 27017:27017 \
  --name mongo \
  mongo:latest
```

---

## Build Backend Image

```bash
cd backend
```

```bash
docker build -t full-stack_backend .
```

---

## Run Backend Container

```bash
docker run -d \
  --network=full-stack \
  --add-host=host.docker.internal:host-gateway \
  -p 5001:5001 \
  --env-file .env \
  full-stack_backend
```

Backend API:

```text
http://localhost:5001
```

---

# ☸️ Kubernetes Deployment

The application is designed around a Kubernetes-based three-tier architecture.

The Kubernetes deployment separates the application into independent workloads:

```text
                    Kubernetes Cluster
                           │
                           ▼
                  ┌─────────────────┐
                  │    Namespace    │
                  │    chat-app     │
                  └───────┬─────────┘
                          │
          ┌───────────────┼────────────────┐
          │               │                │
          ▼               ▼                ▼
   ┌────────────┐  ┌────────────┐   ┌────────────┐
   │  Frontend  │  │  Backend   │   │  MongoDB   │
   │ Deployment │  │ Deployment │   │ Deployment │
   └──────┬─────┘  └──────┬─────┘   └──────┬─────┘
          │               │                │
          ▼               ▼                ▼
   ┌────────────┐  ┌────────────┐   ┌────────────┐
   │ Frontend   │  │ Backend    │   │ MongoDB    │
   │  Service   │  │  Service   │   │  Service   │
   └────────────┘  └────────────┘   └────────────┘
```

### Kubernetes Components

The deployment uses Kubernetes resources such as:

* Namespace
* Deployments
* Services
* Pods
* ConfigMaps
* Secrets
* Persistent Volumes / Persistent Volume Claims

---

# 🔍 Kubernetes Verification

Check the cluster:

```bash
kubectl get nodes
```

Check the application namespace:

```bash
kubectl get all -n chat-app
```

Check pods:

```bash
kubectl get pods -n chat-app
```

Check services:

```bash
kubectl get svc -n chat-app
```

Check deployments:

```bash
kubectl get deployments -n chat-app
```

View pod logs:

```bash
kubectl logs <pod-name> -n chat-app
```

Describe a pod:

```bash
kubectl describe pod <pod-name> -n chat-app
```

---

# 🌐 Service Communication

Kubernetes Services provide stable network endpoints for the application components.

The communication flow is:

```text
Browser
   │
   ▼
Frontend Service
   │
   ▼
Frontend Pods
   │
   │ HTTP / WebSocket
   ▼
Backend Service
   │
   ▼
Backend Pods
   │
   │ MongoDB Protocol
   ▼
MongoDB Service
   │
   ▼
MongoDB Pod
```

Instead of relying on Pod IP addresses, services provide stable DNS-based communication inside the Kubernetes cluster.

---

# 📊 Three-Tier Architecture

## Presentation Tier

**Technology:** React + Nginx

Responsibilities:

* User interface
* User interaction
* API communication
* WebSocket communication

---

## Application Tier

**Technology:** Node.js + Express.js + Socket.io

Responsibilities:

* Business logic
* Authentication
* REST APIs
* WebSocket communication
* User management
* Message processing

---

## Data Tier

**Technology:** MongoDB

Responsibilities:

* Persistent data storage
* User information
* Chat messages
* Application data

---

# 🔐 Security

The application implements JWT-based authentication.

Authentication workflow:

```text
User
 │
 │ Login
 ▼
Frontend
 │
 │ Credentials
 ▼
Backend
 │
 │ Validate User
 ▼
MongoDB
 │
 │ User Data
 ▼
Backend
 │
 │ JWT
 ▼
Frontend
```

The JWT token is then used to authenticate protected API requests.

For Kubernetes production deployments, sensitive configuration such as:

* JWT secrets
* Database credentials
* API keys

should be managed using **Kubernetes Secrets** rather than storing them directly in deployment manifests.

---

# 📈 Scalability

One of the main advantages of using Kubernetes is the ability to scale application workloads independently.

For example:

```bash
kubectl scale deployment backend --replicas=3 -n chat-app
```

The architecture can then run multiple backend Pods:

```text
                Backend Service
                       │
          ┌────────────┼────────────┐
          ▼            ▼            ▼
      Backend-1    Backend-2    Backend-3
         Pod          Pod          Pod
```

The Kubernetes Service distributes traffic between the available Pods.

---

# 🛠️ Troubleshooting Commands

### Check Pod Status

```bash
kubectl get pods -n chat-app
```

### Check Pod Events

```bash
kubectl describe pod <pod-name> -n chat-app
```

### Check Logs

```bash
kubectl logs <pod-name> -n chat-app
```

### Follow Logs

```bash
kubectl logs -f <pod-name> -n chat-app
```

### Check Services

```bash
kubectl get svc -n chat-app
```

### Check Deployments

```bash
kubectl get deployments -n chat-app
```

### Check All Resources

```bash
kubectl get all -n chat-app
```

# 📚 Key DevOps Concepts Demonstrated

* Containerization with Docker
* Dockerfile creation
* Docker image management
* Docker networking
* Docker Compose
* Three-tier architecture
* Kubernetes Deployments
* Kubernetes Services
* Kubernetes Pods
* Kubernetes Namespaces
* Service discovery
* Container orchestration
* Application scaling
* Persistent database storage
* Environment configuration
* JWT-based authentication
* Kubernetes troubleshooting
* REST API deployment
* WebSocket deployment
* Nginx

---

# 🔮 Future Improvements

* [ ] Implement CI/CD using Jenkins or GitHub Actions
* [ ] Add Kubernetes ConfigMaps and Secrets
* [ ] Add Kubernetes Health Checks and Probes
* [ ] Implement Horizontal Pod Autoscaling
* [ ] Add Kubernetes Ingress
* [ ] Add TLS/HTTPS
* [ ] Implement centralized logging
* [ ] Add Prometheus and Grafana monitoring
* [ ] Deploy the application to AWS
* [ ] Use managed MongoDB for production
* [ ] Implement rolling deployments

---

# 📸 Project Screenshots

### Login

![Login](frontend/public/login.png)

### Chat Application

![Chat](frontend/public/chat.png)

### Settings

![Settings](frontend/public/settings.png)

### Logout

![Logout](frontend/public/logout.png)

---

## ⭐ Project Summary

This project demonstrates the complete journey of a full-stack application from **development and containerization to Kubernetes-based deployment**.

```text
MERN Application
       │
       ▼
   Docker
       │
       ▼
 Docker Compose
       │
       ▼
 Kubernetes
       │
       ├── Frontend
       ├── Backend
       └── MongoDB
```

The primary DevOps objective is to create a **reproducible, scalable, and maintainable deployment architecture** for a real-time full-stack application.
