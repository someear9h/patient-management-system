# Patient Management System – Cloud-Native Microservices Architecture

A production-grade **backend microservices system** for managing patients, billing, authentication, and analytics using **Java (Spring Boot)**.  

Built using **modern cloud-native practices** — includes **Kafka, gRPC, Docker, API Gateway, JWT Auth, integration tests**, and attempted **AWS deployment using LocalStack**.

> This project mirrors how scalable distributed systems work in real-world MNCs and startups.

---

## 🚀 Tech Stack

| Category       | Tools / Frameworks                         |
|----------------|--------------------------------------------|
| Language       | Java 21, Spring Boot                       |
| Communication  | gRPC, Kafka                                |
| Auth           | JWT, Spring Security                       |
| API Gateway    | Spring Cloud Gateway                       |
| Containers     | Docker (multi-stage builds)                |
| Testing        | JUnit, Mockito, Integration Testing        |
| Docs           | OpenAPI / Swagger                          |
| Deployment     | Docker Compose, AWS ECS via LocalStack *(attempted)* |
| Infra-as-Code  | AWS CloudFormation                         |

---

## 🧩 Microservices Overview

### 1. **Patient Service**
- CRUD operations on patients
- Kafka Producer for patient events
- gRPC client for billing service
- JWT protected endpoints
- Unit & Integration tested

### 2. **Billing Service**
- Receives billing events via gRPC
- gRPC server implementation
- Dockerized & independently deployable

### 3. **Analytics Service**
- Kafka Consumer for patient events
- Real-time analytics processing
- Fully dockerized

### 4. **Auth Service**
- Login & JWT generation
- Token validation endpoint
- Spring Security + BCrypt password encoding
- Integrated with API Gateway

### 5. **API Gateway**
- Routes requests to all services
- Applies JWT validation filter
- Supports route-based and auth-based restrictions

---

## 📦 Kafka Event Flow

- **Patient Service** → publishes `PatientCreatedEvent` to Kafka
- **Analytics Service** → consumes and processes this event
- Proto-based schema management ensures contract safety

---

## 📡 gRPC Integration

- `PatientService` uses gRPC to call `BillingService`
- Proto files shared via dedicated module
- Efficient binary communication

---

## 🔐 Authentication Flow

- `AuthService` issues JWT on successful login
- API Gateway validates tokens on incoming requests
- Secure communication across all protected routes

---

## 🧪 Testing Coverage

- Unit tests for all services
- Integration tests for:
    - Login
    - Token validation
    - Get patients (auth protected)

---

## ☁️ AWS & Deployment

> Deployment attempted using **AWS LocalStack**, ECS, CloudFormation (IaC)

### Infrastructure Includes:
- ✅ VPC, Subnets
- ✅ RDS Databases
- ✅ MSK (Kafka) Cluster
- ✅ ECS Services & Task Definitions
- ✅ Application Load Balancer
- ✅ Health Checks & Service Discovery

> ⚠️ Note: Deployment was done up to image building & ECS setup; container-level launch via LocalStack ECS requires further fixes due to mock environment limitations.

---

## 🐳 Docker

- Each service has its own `Dockerfile` (multi-stage)
- Ready to deploy on ECS or Kubernetes

---


---

## 🧠 Key Learning Highlights

- Implemented **event-driven architecture** with Kafka
- Built **efficient inter-service RPC** with gRPC
- Designed secure, token-based auth system
- Created **cloud-ready containers**
- Practiced **Infrastructure-as-Code** with CloudFormation
- Understood **real-world deployment complexities** using LocalStack (ECS, MSK, ALB)

---

## 📌 How to Run Locally

```bash
# Clone the repo
git clone https://github.com/your-username/patient-management-system.git
cd patient-management-system

# Start all containers
docker-compose up --build

# Access gateway at
http://localhost:8080/api/patients


