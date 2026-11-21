<div align="center">
  <img src="frontend/src/assets/logo.png" alt="CRTV-ZONE Logo" width="160" />

  <h1>CRTV-ZONE</h1>

  <p>
    <strong>Full-Stack Creative Portfolio, Service Marketplace &amp; Commission Management Platform</strong>
  </p>

  <p>
    <img src="https://img.shields.io/badge/Java-17+-111827?style=for-the-badge&logo=openjdk&logoColor=white" alt="Java" />
    <img src="https://img.shields.io/badge/Spring_Boot-REST_API-111827?style=for-the-badge&logo=springboot&logoColor=6DB33F" alt="Spring Boot" />
    <img src="https://img.shields.io/badge/React-SPA-111827?style=for-the-badge&logo=react&logoColor=61DAFB" alt="React" />
    <img src="https://img.shields.io/badge/JWT-Auth-111827?style=for-the-badge&logo=jsonwebtokens&logoColor=white" alt="JWT" />
    <img src="https://img.shields.io/badge/Supabase-Storage-111827?style=for-the-badge&logo=supabase&logoColor=3ECF8E" alt="Supabase" />
    <img src="https://img.shields.io/badge/Docker-Ready-111827?style=for-the-badge&logo=docker&logoColor=2496ED" alt="Docker" />
  </p>

  <p>
    <a href="#overview">Overview</a> &bull;
    <a href="#core-capabilities">Core Capabilities</a> &bull;
    <a href="#architecture-and-tech-stack">Architecture</a> &bull;
    <a href="#project-structure">Project Structure</a> &bull;
    <a href="#getting-started">Getting Started</a>
  </p>
</div>

---

## Overview

**CRTV-ZONE** is a full-stack web application engineered to streamline how independent artists and creative professionals showcase their work, manage service offerings, and handle client commissions.

The system separates public discovery, client booking operations, and administrative management into distinct, role-protected modules. Powered by a layered **Spring Boot** REST API and a component-driven **React** single-page application, CRTV-ZONE centralizes portfolio curation, resume credentials, booking lifecycles, payment tracking, and client reviews in a single cohesive workspace.

## Core Capabilities

### Artist & Admin Portal

* **Dashboard Overview:** Centralized operational metrics and activity summaries powered by dedicated statistics DTOs.
* **Portfolio & Resume Management:** Full CRUD management for portfolio showcases alongside structured professional credentials, including Experience, Education, Skills, and Achievements.
* **Service Catalog Administration:** Create, configure, inspect, and maintain bookable creative services.
* **Booking Oversight:** Review incoming client requests, inspect detailed booking records, track payment records, and manage fulfillment statuses.
* **Profile Administration:** Maintain artist identity, biography, and public-facing account details.

### Client Experience

* **Artist Discovery:** Browse creative professionals via the Explore interface and inspect comprehensive artist portfolios, credentials, and published works.
* **Service Browsing & Booking:** View available creative services and submit structured booking requests through a guided booking form.
* **Booking Management:** Track active and historical bookings, inspect individual booking details, and monitor status changes.
* **Reviews & Feedback:** Submit verified reviews and ratings for completed engagements.
* **Notifications:** Receive timely updates on booking activity through an integrated notification dropdown.

### Security & Platform Infrastructure

* **Stateless Authentication:** Token-based authentication using JWT (`JwtUtil`, `JwtAuthFilter`) integrated with Spring Security.
* **Route Protection:** Client-side authentication guards (`RequireAuth`, `PublicRoute`) paired with role-based backend authorization.
* **Centralized Error Handling:** Standardized API error responses via `GlobalExceptionHandler`.
* **Cloud Media Integration:** Asset storage integration backed by `SupabaseService`.
* **Health Monitoring:** Dedicated `/health` endpoint for container orchestration and uptime verification.

## Architecture and Tech Stack

| Layer | Technology | Responsibility |
| ----- | ----- | ----- |
| **Backend Framework** | Java, Spring Boot, Maven | Layered REST API (`Controller` -> `Service` -> `Repository` -> `Entity`) |
| **Security** | Spring Security, JWT | Stateless authentication, request filtering, and role-based access control |
| **Data & Persistence** | Spring Data JPA / Hibernate | Relational domain modeling for Users, Bookings, Payments, Reviews, Portfolio, and Resume entities |
| **Media & Storage** | Supabase | Cloud storage management for portfolio media assets |
| **Frontend Framework** | React, JavaScript | Modular SPA with custom `useAuth` hook and guarded routing |
| **HTTP & Styling** | Axios, CSS Modules | Centralized API client with scoped, maintainable component stylesheets |
| **Containerization** | Docker | Reproducible backend container builds via `Backend/Dockerfile` |

## Project Structure

```text
CRTV-ZONE/
├── Backend/                                  # Spring Boot REST API
│   ├── src/main/java/com/artistportfolio/
│   │   ├── config/                           # SecurityConfig, GlobalExceptionHandler
│   │   ├── controller/                       # Admin, Auth, Client, Public, Notification, Health
│   │   ├── dto/                              # Request/Response contracts (Auth, Booking, Portfolio, etc.)
│   │   ├── entity/                           # JPA Entities (User, Booking, Payment, Review, PortfolioWork, etc.)
│   │   ├── repository/                       # Spring Data JPA repositories
│   │   ├── security/                         # JwtAuthFilter, JwtUtil
│   │   └── service/                          # Business logic & SupabaseService
│   ├── src/main/resources/
│   │   └── application.properties            # Environment & datasource configuration
│   ├── src/test/                             # Backend test suite
│   ├── Dockerfile                            # Backend container definition
│   └── pom.xml                               # Maven project configuration
│
└── frontend/                                 # React Web Application
    ├── public/                               # Static entry point, favicon, manifest
    └── src/
        ├── api/                              # Configured Axios instance
        ├── assets/                           # Brand assets (logo.png)
        ├── components/                       # Shared layouts (Sidebar, ClientNavbar), Modal, Notifications
        ├── hooks/                            # Authentication state hook (useAuth)
        ├── pages/
        │   ├── admin_modules/                # Overview, Bookings, Portfolio, Services, Profile
        │   ├── auth_modules/                 # Login, Register, AuthLayout
        │   └── client_modules/               # Home, Explore, Services, Bookings, ClientProfile
        ├── routes/                           # PublicRoute, RequireAuth guards
        └── styles/                           # Shared CSS modules
```

## API Modules

The backend exposes RESTful endpoints organized across six primary controller domains:

| Controller | Domain Responsibility |
| ----- | ----- |
| `AuthController` | User registration, credential authentication, and JWT issuance |
| `PublicController` | Publicly accessible artist profiles, portfolio works, resume data, and service listings |
| `ClientController` | Client profile management, service bookings, booking history, and review submissions |
| `AdminController` | Artist/Admin dashboard statistics, portfolio/resume CRUD, service management, and booking administration |
| `NotificationController` | Retrieval and status management of user notifications |
| `HealthController` | Service liveness and deployment health checks |

## Getting Started

### Prerequisites

Ensure the following tools are installed in your development environment:

* **Java 17+** (or use the included Maven Wrapper `./mvnw`)
* **Node.js 18+** and **npm**
* **Relational Database** (configured in `Backend/src/main/resources/application.properties`)
* **Supabase Project** (for media storage credentials)
* **Docker** *(optional, for containerized backend deployment)*

### 1. Backend Setup

1. Navigate to the backend directory:

   ```bash
   cd Backend
   ```

2. Configure your database connection, JWT signing secret, and Supabase credentials in `src/main/resources/application.properties` (or pass them via environment variables).

3. Build and run the application using the Maven wrapper:

   ```bash
   ./mvnw spring-boot:run
   ```

   *On Windows:*

   ```cmd
   mvnw.cmd spring-boot:run
   ```

#### Running the Backend with Docker

```bash
cd Backend
docker build -t crtv-zone-backend .
docker run -p 8080:8080 --env-file .env crtv-zone-backend
```

### 2. Frontend Setup

1. Navigate to the frontend directory:

   ```bash
   cd frontend
   ```

2. Install dependencies:

   ```bash
   npm install
   ```

3. Verify the API base URL in `src/api/axios.js` (or configure your `.env` file with `REACT_APP_API_URL` if parameterized) to point to your running Spring Boot server.

4. Start the development server:

   ```bash
   npm start
   ```

5. Build for production:

   ```bash
   npm run build
   ```

## Testing

### Backend Tests

Execute the Spring Boot test suite from the `Backend/` directory:

```bash
cd Backend
./mvnw test
```

### Frontend Tests

Execute the React test runner from the `frontend/` directory:

```bash
cd frontend
npm test
```
