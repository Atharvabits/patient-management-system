# Patient Management System

A comprehensive microservices-based patient management system built with Spring Boot, featuring authentication, patient data management, billing integration, and real-time analytics.

## 🏗️ Architecture Overview

This system implements a modern microservices architecture with the following components:

- **Authentication Service** - JWT-based user authentication and authorization
- **Patient Service** - Core patient data management with CRUD operations
- **Billing Service** - gRPC-based billing and payment processing
- **API Gateway** - Centralized routing and JWT validation
- **Analytics Service** - Real-time event processing with Kafka

## 🚀 Features

### Authentication Service
- JWT token-based authentication
- User registration and login
- Role-based access control (ADMIN, USER)
- Secure password hashing with BCrypt
- H2 in-memory database for development

### Patient Service
- Complete patient lifecycle management
- RESTful API endpoints for CRUD operations
- Data validation with custom validation groups
- Integration with billing service via gRPC
- Event publishing to Kafka for analytics
- PostgreSQL database integration

### Billing Service
- gRPC-based communication
- Billing account management
- Integration with patient service
- Protocol Buffers for efficient data serialization

### API Gateway
- Centralized request routing
- JWT token validation
- Load balancing and failover
- CORS configuration
- Request/response logging

### Analytics Service
- Real-time event processing
- Kafka consumer for patient lifecycle events
- Data aggregation and reporting
- Event-driven architecture

## 🛠️ Technology Stack

- **Framework**: Spring Boot 3.x
- **Language**: Java 17+
- **Database**: PostgreSQL (Production), H2 (Development)
- **Message Broker**: Apache Kafka
- **Communication**: REST APIs, gRPC
- **Authentication**: JWT (JSON Web Tokens)
- **Containerization**: Docker
- **Build Tool**: Maven
- **Testing**: JUnit 5, Spring Boot Test

## 📋 Prerequisites

- Java 17 or higher
- Maven 3.8+
- Docker and Docker Compose
- PostgreSQL (for production)
- Apache Kafka

## 🚀 Quick Start

### 1. Clone the Repository
```bash
git clone https://github.com/Atharvabits/patient-management-system.git
cd patient-management-system
```

### 2. Build All Services
```bash
mvn clean install
```

### 3. Start Infrastructure Services
```bash
docker-compose up -d postgres kafka zookeeper
```

### 4. Start Microservices
```bash
# Start Authentication Service
cd auth-service
mvn spring-boot:run

# Start Patient Service
cd ../patient-service
mvn spring-boot:run

# Start Billing Service
cd ../billing-service
mvn spring-boot:run

# Start API Gateway
cd ../api-gateway
mvn spring-boot:run

# Start Analytics Service
cd ../analytics-service
mvn spring-boot:run
```

## 🔧 Configuration

### Environment Variables

#### Authentication Service
```bash
SPRING_DATASOURCE_URL=jdbc:postgresql://localhost:5432/auth_db
SPRING_DATASOURCE_USERNAME=admin_user
SPRING_DATASOURCE_PASSWORD=password
JWT_SECRET=mySecretKey
JWT_EXPIRATION=86400000
```

#### Patient Service
```bash
SPRING_DATASOURCE_URL=jdbc:postgresql://localhost:5432/patient_db
SPRING_DATASOURCE_USERNAME=admin_user
SPRING_DATASOURCE_PASSWORD=password
BILLING_SERVICE_ADDRESS=localhost
BILLING_SERVICE_GRPC_PORT=9005
SPRING_KAFKA_BOOTSTRAP_SERVERS=localhost:9092
```

#### Billing Service
```bash
GRPC_SERVER_PORT=9005
```

#### Analytics Service
```bash
SPRING_KAFKA_BOOTSTRAP_SERVERS=localhost:9092
KAFKA_TOPIC_PATIENT_EVENTS=patient-lifecycle-events
```

## 📚 API Documentation

### Authentication Endpoints
- `POST /api/auth/login` - User login
- `POST /api/auth/register` - User registration
- `POST /api/auth/validate` - Token validation

### Patient Management Endpoints
- `GET /api/patients` - Get all patients
- `GET /api/patients/{id}` - Get patient by ID
- `POST /api/patients` - Create new patient
- `PUT /api/patients/{id}` - Update patient
- `DELETE /api/patients/{id}` - Delete patient

### Billing Endpoints (gRPC)
- `CreateBillingAccount` - Create billing account
- `GetBillingInfo` - Retrieve billing information
- `UpdateBillingAccount` - Update billing details

## 🧪 Testing

### Run Unit Tests
```bash
mvn test
```

### Run Integration Tests
```bash
cd integration-tests
mvn test
```

### API Testing
Use the provided HTTP files in the `api-requests` directory with your favorite HTTP client (IntelliJ HTTP Client, Postman, etc.).

## 🐳 Docker Support

Each service includes a Dockerfile for containerization:

```bash
# Build Docker images
docker build -t auth-service ./auth-service
docker build -t patient-service ./patient-service
docker build -t billing-service ./billing-service
docker build -t api-gateway ./api-gateway
docker build -t analytics-service ./analytics-service
```

## 🏛️ Database Schema

### Users Table (Authentication Service)
```sql
CREATE TABLE users (
    id UUID PRIMARY KEY,
    email VARCHAR(255) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    role VARCHAR(50) NOT NULL
);
```

### Patients Table (Patient Service)
```sql
CREATE TABLE patients (
    id UUID PRIMARY KEY,
    first_name VARCHAR(255) NOT NULL,
    last_name VARCHAR(255) NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    phone VARCHAR(20),
    date_of_birth DATE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## 🔄 Event Flow

1. **Patient Registration**: Patient service publishes `PatientCreated` event to Kafka
2. **Billing Integration**: Patient service calls billing service via gRPC for account setup
3. **Analytics Processing**: Analytics service consumes events for real-time reporting
4. **Authentication**: All requests pass through API gateway for JWT validation

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Spring Boot team for the excellent framework
- Apache Kafka for reliable event streaming
- gRPC for efficient inter-service communication
- PostgreSQL for robust data persistence

## 📞 Support

For questions and support, please open an issue in the GitHub repository.

---

**Built with ❤️ using Spring Boot and modern microservices architecture**