# 🏥 MediCore Hospital Management System

### A Full-Stack Platform for Managing Patients, Doctors, Appointments & Billing



[Backend
Repository](https://github.com/ashrithBalaji456/Hospital-Backend) •
[Frontend
Repository](https://github.com/ashrithBalaji456/Hospital-Frontend)
:::

------------------------------------------------------------------------

## 📌 Overview

**MediCore Hospital Management System** is a full-stack application
designed to digitize and simplify core hospital operations through a
centralized platform.

The system connects a modern frontend with a Spring Boot REST API and
PostgreSQL database to manage the operational lifecycle of a hospital:

-   👤 Patient registration and records
-   👨‍⚕️ Doctor information and availability
-   📅 Appointment booking and management
-   💳 Billing and payment records
-   📊 Operational data through a unified interface

The project demonstrates REST API design, layered backend architecture,
relational database modelling, frontend-backend integration, validation,
persistence, and production-oriented health monitoring.

> \[!NOTE\] This is a portfolio and learning project. It is not intended
> for real clinical use or storage of actual sensitive medical records
> without additional security, privacy, audit, and regulatory controls.

------------------------------------------------------------------------

## ✨ Core Features

### 👤 Patient Management

-   Register new patients.
-   View patient records.
-   Update patient information.
-   Delete or manage patient records through REST APIs.
-   Associate patients with appointments and billing workflows.

### 👨‍⚕️ Doctor Management

-   Add and maintain doctor information.
-   Store specialization and professional details.
-   View available doctors.
-   Connect doctors with patient appointments.
-   Maintain doctor-related hospital records.

### 📅 Appointment Management

-   Create appointments between patients and doctors.
-   Track appointment details.
-   Update appointment information and status.
-   View scheduled appointments.
-   Maintain relationships between patients, doctors, and appointments.

### 💳 Billing Management

-   Create billing records.
-   Associate billing information with hospital workflows.
-   Track payment-related information.
-   Maintain billing history in PostgreSQL.

### 🌐 Full-Stack Integration

-   Frontend communicates with the backend through REST APIs.
-   Backend validates requests and executes business rules.
-   Spring Data JPA handles database persistence.
-   PostgreSQL stores structured hospital data.
-   JSON responses are returned to the frontend for presentation.

------------------------------------------------------------------------

## 🧰 Technology Stack

  Layer                   Technology
  ----------------------- -------------------------------
  Backend Language        Java 17
  Backend Framework       Spring Boot 4.0.5
  Web Layer               Spring Web MVC / REST APIs
  ORM                     Spring Data JPA, Hibernate
  Database                PostgreSQL
  Monitoring              Spring Boot Actuator
  Boilerplate Reduction   Lombok
  Build Tool              Maven
  Frontend                Separate frontend application
  API Testing             Postman
  Version Control         Git & GitHub

------------------------------------------------------------------------

## 🏗️ System Architecture

``` mermaid
flowchart LR
    U[Hospital Staff / User] --> FE[Frontend Application]
    FE -->|HTTP / JSON| API[Spring Boot REST API]

    API --> PC[Patient Controller]
    API --> DC[Doctor Controller]
    API --> AC[Appointment Controller]
    API --> BC[Billing Controller]

    PC --> PS[Patient Service]
    DC --> DS[Doctor Service]
    AC --> AS[Appointment Service]
    BC --> BS[Billing Service]

    PS --> PR[Patient Repository]
    DS --> DR[Doctor Repository]
    AS --> AR[Appointment Repository]
    BS --> BR[Billing Repository]

    PR --> DB[(PostgreSQL)]
    DR --> DB
    AR --> DB
    BR --> DB

    ACT[Spring Boot Actuator] --> API
```

------------------------------------------------------------------------

## 🔄 Complete Application Workflow

``` mermaid
flowchart TD
    A[User Opens Frontend] --> B[Frontend Loads Hospital Dashboard]
    B --> C{Select Module}

    C -->|Patients| D[Patient Management]
    C -->|Doctors| E[Doctor Management]
    C -->|Appointments| F[Appointment Management]
    C -->|Billing| G[Billing Management]

    D --> H[REST API Request]
    E --> H
    F --> H
    G --> H

    H --> I[Controller Layer]
    I --> J[Service Layer]
    J --> K[Business Logic & Validation]
    K --> L[Repository Layer]
    L --> M[(PostgreSQL)]

    M --> N[JPA Entity / Result]
    N --> O[Service Response]
    O --> P[JSON API Response]
    P --> Q[Frontend Updates UI]
```

### Step-by-Step Flow

1.  The user opens the frontend application.
2.  The frontend displays hospital-management modules.
3.  The user performs an action such as registering a patient, adding a
    doctor, booking an appointment, or managing billing.
4.  The frontend sends an HTTP request to the appropriate backend REST
    endpoint.
5.  The controller accepts the request and delegates processing to the
    service layer.
6.  The service layer applies business logic and coordinates data
    access.
7.  The repository layer communicates with PostgreSQL through Spring
    Data JPA and Hibernate.
8.  The database result travels back through Repository → Service →
    Controller.
9.  The backend returns a JSON response.
10. The frontend updates the interface with the latest information.

------------------------------------------------------------------------

## 🧱 Backend Layered Architecture

``` text
Hospital-Backend/
│
├── controller/
│   ├── PatientController
│   ├── DoctorController
│   ├── AppointmentController
│   └── BillingController
│
├── service/
│   ├── PatientService
│   ├── DoctorService
│   ├── AppointmentService
│   └── BillingService
│
├── repository/
│   ├── PatientRepository
│   ├── DoctorRepository
│   ├── AppointmentRepository
│   └── BillingRepository
│
├── entity/
│   ├── Patient
│   ├── Doctor
│   ├── Appointment
│   └── Billing
│
└── HospitalManagementSystemApplication.java
```

The project follows a layered architecture:

``` mermaid
flowchart LR
    C[Controller] --> S[Service]
    S --> R[Repository]
    R --> DB[(PostgreSQL)]
    DB --> R
    R --> S
    S --> C
```

  Layer        Responsibility
  ------------ ----------------------------------------------------
  Controller   Receives HTTP requests and returns responses
  Service      Contains business logic and coordinates operations
  Repository   Handles database access using Spring Data JPA
  Entity       Maps Java objects to relational tables
  Database     Stores persistent hospital data

------------------------------------------------------------------------

## 🗃️ Conceptual Data Model

``` mermaid
erDiagram
    PATIENT ||--o{ APPOINTMENT : books
    DOCTOR ||--o{ APPOINTMENT : attends
    PATIENT ||--o{ BILLING : receives
    APPOINTMENT ||--o| BILLING : may_generate

    PATIENT {
        bigint id PK
        string name
        string gender
        string contact
        string address
    }

    DOCTOR {
        bigint id PK
        string name
        string specialization
        string contact
    }

    APPOINTMENT {
        bigint id PK
        bigint patient_id FK
        bigint doctor_id FK
        datetime appointment_time
        string status
    }

    BILLING {
        bigint id PK
        bigint patient_id FK
        decimal amount
        string payment_status
        datetime created_at
    }
```

> The diagram represents the logical hospital workflow. Keep the entity
> field names in sync with the actual implementation as the project
> evolves.

------------------------------------------------------------------------

## 📡 REST API Design

A clean API organization for the platform:

  Module         Base Endpoint         Operations
  -------------- --------------------- ---------------------------------
  Patients       `/api/patients`       Create, read, update, delete
  Doctors        `/api/doctors`        Create, read, update, delete
  Appointments   `/api/appointments`   Book, view, update, cancel
  Billing        `/api/billing`        Create and view billing records
  Health         `/actuator/health`    Application health monitoring

Example request flow:

``` text
POST /api/appointments
        ↓
AppointmentController
        ↓
AppointmentService
        ↓
Validate Patient + Doctor
        ↓
AppointmentRepository
        ↓
PostgreSQL
        ↓
JSON Response
```

------------------------------------------------------------------------

## 🚀 Getting Started

### Prerequisites

Install:

-   Java 17+
-   Maven
-   PostgreSQL
-   Node.js and npm if required by the frontend
-   Git

### 1. Clone the Backend

``` bash
git clone https://github.com/ashrithBalaji456/Hospital-Backend.git
cd Hospital-Backend
```

### 2. Create PostgreSQL Database

``` sql
CREATE DATABASE hospital_db;
```

### 3. Configure Database Connection

Use environment variables or your local Spring configuration:

``` properties
spring.datasource.url=jdbc:postgresql://localhost:5432/hospital_db
spring.datasource.username=postgres
spring.datasource.password=your_password

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
```

> \[!WARNING\] Never commit real database passwords or production
> credentials to GitHub.

### 4. Run the Backend

On Linux/macOS:

``` bash
./mvnw spring-boot:run
```

On Windows:

``` bash
mvnw.cmd spring-boot:run
```

Or, if Maven is installed globally:

``` bash
mvn spring-boot:run
```

### 5. Clone the Frontend

Open another terminal:

``` bash
git clone https://github.com/ashrithBalaji456/Hospital-Frontend.git
cd Hospital-Frontend
```

Install and run using the commands required by the frontend project
configuration.

------------------------------------------------------------------------

## 🧪 API Testing Flow

The API can be tested with Postman:

``` mermaid
sequenceDiagram
    participant P as Postman / Frontend
    participant C as REST Controller
    participant S as Service Layer
    participant R as JPA Repository
    participant DB as PostgreSQL

    P->>C: HTTP Request + JSON
    C->>S: Delegate operation
    S->>R: Persistence operation
    R->>DB: SQL via Hibernate
    DB-->>R: Result
    R-->>S: Entity / Collection
    S-->>C: Processed result
    C-->>P: HTTP Status + JSON
```

Recommended testing order:

1.  Create a doctor.
2.  Create a patient.
3.  Fetch and verify both records.
4.  Create an appointment linking the patient and doctor.
5.  Update appointment status.
6.  Create the related billing record.
7.  Verify patient, appointment, and billing data.

------------------------------------------------------------------------

## 📊 Monitoring with Spring Boot Actuator

The backend includes Spring Boot Actuator for application observability.

Typical health endpoint:

``` text
GET /actuator/health
```

Example response:

``` json
{
  "status": "UP"
}
```

Actuator can later be extended with metrics and monitoring integrations.

------------------------------------------------------------------------

## 🔐 Production Improvements

For a real-world healthcare environment, the following would be
essential:

-   Spring Security authentication.
-   Role-based access control for Admin, Doctor, Receptionist, and
    Billing Staff.
-   JWT or secure session authentication.
-   Encryption of sensitive data.
-   Audit logging for record access and modification.
-   Strong request validation.
-   Rate limiting.
-   Secure secret management.
-   HTTPS everywhere.
-   Database backups and disaster recovery.
-   Applicable privacy and healthcare regulatory compliance.

------------------------------------------------------------------------

## 🧪 Testing Strategy

Recommended coverage:

-   Service-layer unit tests.
-   Repository integration tests.
-   Controller/API integration tests.
-   Patient CRUD tests.
-   Doctor CRUD tests.
-   Appointment relationship tests.
-   Billing calculation and persistence tests.
-   Invalid-ID and missing-resource tests.
-   PostgreSQL integration tests using Testcontainers.
-   Frontend API integration tests.

------------------------------------------------------------------------

## 🧠 Engineering Concepts Demonstrated

-   RESTful API design
-   Layered architecture
-   Dependency injection
-   Object-relational mapping
-   Entity relationships
-   Repository pattern
-   Service-layer business logic
-   PostgreSQL integration
-   Frontend-backend communication
-   JSON request/response handling
-   CRUD operations
-   Maven dependency management
-   Application health monitoring

------------------------------------------------------------------------

## 🗺️ Future Enhancements

-   [ ] Spring Security with JWT authentication
-   [ ] Role-based authorization
-   [ ] Admin dashboard analytics
-   [ ] Doctor availability scheduling
-   [ ] Appointment reminders through email/SMS
-   [ ] Prescription management
-   [ ] Medical record document upload
-   [ ] Search, filtering, sorting, and pagination
-   [ ] Global exception handling with consistent error responses
-   [ ] DTO mapping layer
-   [ ] OpenAPI / Swagger documentation
-   [ ] Flyway database migrations
-   [ ] Docker and Docker Compose
-   [ ] CI/CD using GitHub Actions
-   [ ] Testcontainers for PostgreSQL integration tests
-   [ ] Cloud deployment with managed PostgreSQL

------------------------------------------------------------------------

## 📂 Project Repositories

  ----------------------------------------------------------------------------------------------------------------
  Component                           Repository
  ----------------------------------- ----------------------------------------------------------------------------
  ⚙️ Backend                          [Hospital-Backend](https://github.com/ashrithBalaji456/Hospital-Backend)

  🎨 Frontend                         [Hospital-Frontend](https://github.com/ashrithBalaji456/Hospital-Frontend)
  ----------------------------------------------------------------------------------------------------------------

------------------------------------------------------------------------

## 👨‍💻 Author

**Gudla Ashrith Balaji**

Java Backend Developer focused on Spring Boot, REST APIs, PostgreSQL,
and full-stack application development.

-   LinkedIn:
    https://www.linkedin.com/in/ashrith-balaji-gudla-5768302a8/
-   GitHub: https://github.com/ashrithBalaji456

------------------------------------------------------------------------

## ⭐ Support

If you find the project useful, consider starring the repositories.


### Built with ☕ Java • 🌱 Spring Boot • 🐘 PostgreSQL

**Better workflows. Cleaner architecture. Smarter hospital operations.**

