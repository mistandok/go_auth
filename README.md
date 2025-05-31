# Auth Microservice

A comprehensive authentication and authorization microservice built with Go, gRPC, and PostgreSQL. This service provides user management, authentication, and access control functionality with modern observability features.

## 🚀 Features

- **User Management**: Complete user lifecycle management with CRUD operations
- **Authentication**: JWT-based authentication with secure token handling
- **Authorization**: Role-based access control (RBAC) system
- **gRPC API**: High-performance gRPC service with HTTP gateway support
- **OpenAPI Documentation**: Auto-generated Swagger documentation
- **Observability**: Integrated monitoring with Prometheus, Grafana, and Jaeger tracing
- **Database Migrations**: Automated database schema management
- **Redis Cache**: Session and token caching support
- **Docker Support**: Complete containerization with docker-compose

## 🏗️ Architecture

The service is built using clean architecture principles with the following components:

- **API Layer**: gRPC services with HTTP gateway (user_v1, auth_v1, access_v1)
- **Service Layer**: Business logic implementation
- **Repository Layer**: Data access abstraction
- **Database**: PostgreSQL for persistent storage
- **Cache**: Redis for session management
- **Monitoring**: Prometheus metrics, Grafana dashboards, Jaeger tracing

## 📋 Prerequisites

Before running the service, ensure you have:

- **Docker** and **Docker Compose** installed
- **Go 1.21.3+** (for local development)
- **Make** utility
- **PostgreSQL** (if running without Docker)
- **Redis** (if running without Docker)

## 🛠️ Installation & Setup

### 1. Clone the Repository

```bash
git clone https://github.com/mistandok/auth.git
cd auth
```

### 2. Install Dependencies

```bash
make install-deps
```

This will install all required tools including:
- Protocol Buffers compiler
- gRPC tools
- Linting tools
- Migration tools
- Code generation tools

### 3. Generate Proto Files

```bash
make vendor-proto
make generate
```

## 🚀 Running the Service

### Option 1: Using Docker Compose (Recommended)

#### Local Development

```bash
# Start all services (includes PostgreSQL, Redis, monitoring stack)
make local-start-app

# Stop all services
make local-down-app
```

#### Production

```bash
# Start production environment
make prod-start-app

# Stop production environment
make prod-down-app
```

### Option 2: Running Locally

1. **Setup Environment Variables**
   ```bash
   make setup-local-env
   ```

2. **Start Dependencies** (PostgreSQL, Redis)
   ```bash
   # Start only infrastructure services
   docker-compose -f docker-compose.local.yaml up storage redis -d
   ```

3. **Run Database Migrations**
   ```bash
   make local-migration-up
   ```

4. **Start the Service**
   ```bash
   go run cmd/service/main.go
   ```

## 🗄️ Database Management

### Migrations

```bash
# Check migration status
make local-migration-status

# Apply migrations
make local-migration-up

# Rollback migrations
make local-migration-down

# Create new migration
make local-create-new-migration migration_name=your_migration_name
```

## 🔧 Development

### Code Generation

```bash
# Generate all proto files and swagger docs
make generate

# Generate specific API
make generate-user-api
make generate-auth-api
make generate-access-api
```

### Testing

```bash
# Run tests
make test

# Run tests with coverage
make test-coverage
```

### Code Quality

```bash
# Run linter
make lint

# Fix import formatting
make fix-imports
```

## 📊 Monitoring & Observability

When running with docker-compose, the following monitoring tools are available:

- **Prometheus**: http://localhost:9090 - Metrics collection
- **Grafana**: http://localhost:3000 - Dashboards and visualization
- **Jaeger**: http://localhost:16686 - Distributed tracing

## 📚 API Documentation

The service provides three main APIs:

1. **User API** (`user_v1`): User management operations
2. **Auth API** (`auth_v1`): Authentication operations
3. **Access API** (`access_v1`): Authorization and access control

### Swagger Documentation

After starting the service, OpenAPI/Swagger documentation is available at:
- Swagger UI: http://localhost:8080/swagger/ (when HTTP gateway is enabled)

### gRPC APIs

The service exposes gRPC endpoints on the configured port with support for:
- Server reflection
- Health checks
- Metrics export

## 🔒 Security

- JWT-based authentication
- Password hashing with bcrypt
- Role-based access control
- Secure token storage in Redis
- Environment-based configuration

## 🏃‍♂️ Quick Start

1. **Start the entire stack**:
   ```bash
   make local-start-app
   ```

2. **Check if everything is running**:
   ```bash
   docker-compose -f docker-compose.local.yaml ps
   ```

3. **View logs**:
   ```bash
   docker-compose -f docker-compose.local.yaml logs -f
   ```

4. **Access monitoring tools**:
   - Grafana: http://localhost:3000
   - Prometheus: http://localhost:9090
   - Jaeger: http://localhost:16686

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Run tests and linting
5. Submit a pull request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
