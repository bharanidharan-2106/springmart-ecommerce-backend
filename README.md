# SpringMart Backend Project

## Role-Based Multi-Vendor E-Commerce System  
Built using **Spring Boot, Spring Security, JWT & MySQL**


A production-style, role-based multi-vendor e-commerce backend system built using Spring Boot, Spring Security (JWT), and MySQL. The application simulates a real-world marketplace platform with secure authentication, modular architecture, and domain-driven design.

---

## Overview

SpringMart is a backend system designed to model a scalable e-commerce platform similar to Amazon or Flipkart. It supports multiple user roles, enforces business rules, and provides secure RESTful APIs for managing products, orders, and user interactions.

The system is built using a layered monolithic architecture with a strong focus on security, maintainability, and real-world applicability.

---

## Key Highlights

* Role-based multi-vendor architecture (Admin, Merchant, Customer)
* JWT-based stateless authentication and authorization
* Fine-grained Role-Based Access Control (RBAC)
* Transactional order processing with stock management
* Merchant approval workflow before system access
* Review and rating system with business rule enforcement
* Clean layered architecture with separation of concerns
* DTO-based API design for structured data exchange

---

## Architecture

Layered Monolithic Architecture:

```text id="yq4f0g"
Controller Layer
        ↓
Service Layer
        ↓
Repository Layer
        ↓
MySQL Database
```

### Layer Responsibilities

| Layer      | Responsibility                                |
| ---------- | --------------------------------------------- |
| Controller | Handles REST API requests and responses       |
| Service    | Business logic and validation                 |
| Repository | Data access using JPA/Hibernate               |
| Security   | Authentication and authorization (JWT + RBAC) |

---

## Security Implementation

* Stateless authentication using JWT
* Password encryption using BCrypt
* Role-based authorization via Spring Security
* Secured API endpoints based on user roles
* CSRF disabled for REST APIs
* Centralized exception handling

### Role-Based Access Example

```java id="8wslq6"
.requestMatchers("/api/admin/**").hasRole("ADMIN")
.requestMatchers("/api/merchant/**").hasRole("MERCHANT")
.requestMatchers("/api/customer/**").hasRole("CUSTOMER")
```

---

## User Roles and Capabilities

### Admin

* Approve or reject merchant registrations
* View and manage all users
* Moderate and delete products
* Monitor platform activity

### Merchant

* Add, update, and manage products
* Perform soft delete operations
* Manage inventory and stock levels
* Access merchant-specific orders
* Requires admin approval before activation

### Customer

* Browse and search products
* Manage cart and place orders
* View order history
* Submit reviews (restricted to purchased products)

---

## Core Modules

* Authentication Module (JWT)
* Admin Module
* Merchant Module
* Customer Module
* Cart Module
* Order Module (Transactional)
* Review and Rating Module

---

## Database Design

### Main Entities

* User
* Product
* CartItem
* Order
* OrderItem
* Review
* Role (Enum)

### Key Relationships

* One Merchant → Many Products
* One Customer → Many Orders
* One Order → Many OrderItems
* One Product → Many Reviews
* One Customer → Many CartItems

---

## Business Rules Implemented

* Merchant must be approved before login
* Customers can review only purchased products
* Stock updates automatically after order placement
* Products are deactivated when stock reaches zero
* Soft delete for merchant-owned products
* Hard delete privileges restricted to admin
* JWT required for all protected endpoints
* Role validation enforced at API level

---

## Technology Stack

### Backend

* Java 17
* Spring Boot
* Spring MVC
* Spring Data JPA (Hibernate)

### Security

* Spring Security
* JWT (JSON Web Token)

### Database

* MySQL

### Tools

* Maven
* Postman

---

## Setup and Installation

### 1. Clone Repository

```bash id="u3v7t0"
git clone https://github.com/bharanidharan-2106/springmart-ecommerce-backend.git
cd springmart-ecommerce-backend
```

---

### 2. Configure Database

Create database:

```sql id="b4j2rf"
CREATE DATABASE springmart;
```

---

### 3. Configure Application Properties

Create:

```text id="a0m7rn"
src/main/resources/application.properties
```

Use `application-example.properties` as reference.

Note:
The `application.properties` file is excluded from version control to protect sensitive configuration such as database credentials.

---

### 4. Run the Application

```bash id="6xq1je"
mvn spring-boot:run
```

Application runs at:

```text id="6j5qz4"
http://localhost:8080
```

---

## API Testing

APIs can be tested using:

* Postman

---

## Limitations

* No payment gateway integration
* No image upload support
* No distributed caching
* Monolithic architecture (non-microservices)
* No email notification system

---

## Key Engineering Focus

* Secure backend design using JWT and RBAC
* Real-world domain modeling for e-commerce systems
* Transaction consistency in order processing
* Clean code practices and modular architecture
* Scalable and maintainable backend structure

---


## Note

This project is developed for learning and demonstration purposes, focusing on backend architecture, security implementation, and real-world application design using Spring Boot.


