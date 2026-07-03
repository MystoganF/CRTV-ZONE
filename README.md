Artist Portfolio Platform - Backend API

What is this App About?
This project is a backend REST API designed for an Artist Portfolio and Booking platform. It serves as the core engine connecting artists with potential clients. The platform allows artists to fully showcase their professional identity by managing their skills, education, experience, achievements, and visual portfolio works. Clients can browse public portfolios, book specific artist services, securely process payments, and leave reviews. The system also includes dedicated administrative controls and a real-time notification system. 

Tech Stack
Based on the repository configuration, this project utilizes the following technologies:
Java & Spring Boot: The core framework driving the application architecture.
Maven: Used for dependency management and project builds (pom.xml, mvnw).
Spring Security & JWT: Implements secure, token-based authentication and authorization (SecurityConfig.java, JwtUtil.java, JwtAuthFilter.java).
Spring Data JPA: For database entity management and repository patterns.
Supabase: Integrated as a backend service, likely used for database hosting or seamless file/blob storage (SupabaseService.java).
Docker: Configured for easy containerization and deployment (Dockerfile).

Core Features
Role-Based Access Control: Distinct endpoints and permissions for Admins, Clients, and Public users.
Secure Authentication: User login and registration secured via JSON Web Tokens (JWT).
Portfolio Management: Artists can upload and manage comprehensive portfolios, including visual portfolio works, professional skills, experience, education, and notable achievements.
Service Bookings: A complete booking flow connecting clients to artist services.
Payments Processing: Entity and repository structures in place to track and manage client payments.
Review System: Clients can leave reviews and ratings for artists post-service.
Notification Engine: System to alert users of booking updates, payment statuses, or administrative alerts.
Statistics & Analytics: DTOs structured to deliver platform or artist statistics.

Project Structure Overview
The project follows a standard Spring Boot layered architecture:
config/ - Contains global configurations like CORS, Security, and Global Exception Handling.
controller/ - REST API endpoints separated by domain (Admin, Auth, Client, Public, Notifications).
dto/ - Data Transfer Objects shaping the API requests and responses.
entity/ - JPA domain models mapping directly to database tables (User, Booking, Review, PortfolioWork, etc.).
repository/ - Interfaces for database CRUD operations.
security/ - JWT filters and utilities for protecting routes.
service/ - Contains the core business logic and external integrations (like Supabase).
uploads/portfolio/ - Local directory handling the storage of artist portfolio media.

Getting Started

Prerequisites
Java Development Kit (JDK)
Maven
Docker (Optional, for containerized deployment)
Supabase Account & API Keys

Installation & Setup

Step 1. Clone the repository:
git clone <repository-url>
cd Backend

Step 2. Configure Environment Variables:
Update the src/main/resources/application.properties file with your database credentials, JWT secret, and Supabase API keys.

Step 3. Run the Application Locally:
Using the Maven wrapper included in the project run:
./mvnw spring-boot:run
(For Windows users, use mvnw.cmd spring-boot:run)

Step 4. Run via Docker:
A Dockerfile is provided for containerized deployment. Run:
docker build -t artist-portfolio-backend .
docker run -p 8080:8080 artist-portfolio-backend
