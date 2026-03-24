# Project Document

# HomemadeFoodies – Home-Made Food Marketplace Platform

---

## 1. Project Name
**HomeBite – Home-Made Food Delivery Platform**

---

## 2. Main Motto of the Project

### Primary Goal
To create a platform that connects home cooks (vendors) with customers, enabling them to sell and buy home-made food easily, safely, and affordably.

### Core Mission
- Empower small home cooks to earn income
- Provide customers with authentic home-made food
- Simplify delivery using integrated logistics
- Maintain very low platform commission

### Problem the Project Solves

Many talented home cooks:
- Cannot reach customers
- Lack digital platforms
- Cannot manage delivery and payments

Customers:
- Want hygienic home food
- Cannot easily discover home chefs nearby

This platform solves both problems.

---

## 3. Project Requirements

### Functional Requirements
- **Real-Time Delivery flow**: The system must be capable of supporting the real-time processing, orchestration, and tracking of food deliveries from the moment an order is placed to when it arrives at the customer's door.
- **Vendor Management**: Home cooks must be able to seamlessly register, manage their home-made food menu, and accept or reject incoming orders.
- **Customer Experience**: Customers should have an intuitive interface to discover home-made food, order meals, and make secure online payments.
- **Logistics Integration**: Automated integration with third-party logistics/delivery partners (e.g., Shiprocket) to assign delivery personnel and track shipments dynamically.

### Non-Functional Requirements
- **Scalability**: Utilizing a microservices approach to ensure that high-traffic components (like the Order and User Services) can scale independently.
- **Security & Authorization**: Implement robust role-based access control (Customer, Vendor, Admin) and secure API endpoints using JWT authentication.
- **Reliability**: Ensure the order flow maintains data consistency across services and handles integration failures (like payment drops) gracefully.

---

## 4. Stakeholders
- Vendor (Home Cook)
- Customer (Buyer)
- Delivery Partner (via Shiprocket integration)
- Platform Admin

---

## 5. System Overview

### System Flow
Customer → Orders food  
Platform → Processes payment  
Platform → Notifies vendor  
Delivery partner → Picks and delivers order

### Architecture
Mobile App / Web App
|
API Gateway
|
User Service
Vendor Service
Food Catalog Service
Order Service
Payment Service
Delivery Integration Service


---

## 6. Technology Stack

### Backend
- Spring Boot Microservices
- Spring Cloud Gateway
- Spring Security (JWT)
- MySQL / PostgreSQL
- Redis (optional)

### Frontend
- React (Web App)  
  or
- Flutter / React Native (Mobile App)

### Integrations
- Payment: Razorpay
- Delivery: Shiprocket

Companies like:
- Razorpay
- Shiprocket  
  provide APIs for this.

---

## 7. Backend Development & Build Requirements

### Development Standards
1. **Language & Framework Profile**: 
   - **Java Version**: Java 17+ (LTS).
   - **Frameworks**: Spring Boot 3.x, Spring Cloud.
2. **Architecture Pattern**: Database-per-service approach. Each microservice should have its own database schema or database instance to avoid tight coupling.
3. **API Design**: Pure RESTful APIs using standard HTTP verbs (GET, POST, PUT, DELETE). API boundaries should be defined strongly, and entities should be protected from exposure using DTOs (Data Transfer Objects).
4. **Inter-Service Communication**:
   - **Synchronous**: Spring Cloud OpenFeign for direct, blocking HTTP calls.
   - **Asynchronous**: RabbitMQ or Apache Kafka for event-driven flows (e.g., triggering a background delivery request when an order payment is successfully verified).
5. **Security**: Centralized authentication approach. The API Gateway validates JWTs and delegates secure user context to downstream microservices.

### Build & Deployment Strategy
1. **Build Tool**: Apache Maven (or Gradle) for managing dependencies and multi-module project builds. Provide a parent `pom.xml` to manage common dependency versions.
2. **Containerization**: Provide a `Dockerfile` for each microservice using lightweight base images (e.g., `eclipse-temurin:17-jre-alpine`).
3. **Local Orchestration**: Implement a `docker-compose.yml` file to spin up all required backing services (MySQL, PostgreSQL, Redis, RabbitMQ) and microservices in one go for a smooth developer experience.
4. **CI/CD Integration (Optional)**: Basic GitHub Actions workflows to compile (`mvn clean package`) and run tests upon integration.

---

## 8. User Roles

### 1. Customer

Can:
- Register
- Browse food
- Order food
- Pay online
- Track delivery

### 2. Vendor (Home Cook)

Can:
- Register
- Add food items
- Accept orders
- Manage menu
- View earnings

### 3. Admin

Can:
- Approve vendors
- Monitor orders
- Manage platform

---

## 9. Core Features (Minimum Viable Product)

### Vendor
- Register as vendor
- Add food items
- Set price
- Upload food image
- Accept orders

### Customer
- Sign up / Login
- Browse vendors
- View food items
- Add to cart
- Place order
- Pay using Razorpay

### Platform
- Create order
- Notify vendor
- Create delivery request (Shiprocket)
- Track order

---

## 10. Microservices Breakdown

### 1. User Service
Handles login and registration.

**APIs**
- POST /register
- POST /login
- GET /profile

**Tables**
- users
- roles

---

### 2. Vendor Service
Handles home cooks.

**APIs**
- POST /vendor/register
- GET /vendor/menu
- POST /vendor/add-item

**Tables**
- vendors
- vendor_menu

---

### 3. Food Catalog Service
Stores food items.

**Tables**
- food_items
- categories
- images

---

### 4. Order Service
Handles order flow.

**Tables**
- orders
- order_items
- order_status

**Flow**
Customer order → Vendor notification → Delivery request

---

### 5. Payment Service
Integration with Razorpay.

**Steps**
1. Create payment order
2. Customer pays
3. Verify payment
4. Confirm order

---

### 6. Delivery Service
Integration with Shiprocket.

**Steps**
1. Create shipment
2. Assign courier
3. Track delivery

---

## 11. Product Backlog

### Epic 1 – User System
- User registration
- Login system
- JWT authentication

### Epic 2 – Vendor Platform
- Vendor onboarding
- Vendor approval system
- Add menu items

### Epic 3 – Food Marketplace
- Browse food
- Search food
- View vendor profile

### Epic 4 – Order System
- Add to cart
- Place order
- Order history

### Epic 5 – Payment Integration
- Razorpay integration
- Payment confirmation

### Epic 6 – Delivery Integration
- Shiprocket API integration
- Order tracking

---

## 12. Sprint Backlog Plan

Each sprint = **2 weeks**

### Sprint 1 – Project Setup
- Setup GitHub
- Setup microservices architecture
- Setup API gateway
- Setup database

**Goal:**  
System foundation ready.

---

### Sprint 2 – User & Vendor Registration
- Customer signup
- Vendor signup
- Authentication system

**Goal:**  
Users and vendors can join.

---

### Sprint 3 – Food Listing
- Vendor adds food
- Customer sees menu
- Image upload

**Goal:**  
Marketplace visible.

---

### Sprint 4 – Cart & Order
- Add to cart
- Place order
- Create order record

**Goal:**  
Customers can buy food.

---

### Sprint 5 – Payment Integration
- Integrate Razorpay
- Payment verification

**Goal:**  
Real payment flow working.

---

### Sprint 6 – Delivery Integration
- Connect Shiprocket
- Create delivery request
- Track delivery

**Goal:**  
Full order cycle working.

---

## 13. Database Design (Simplified)

### Users
- id
- name
- email
- password
- role

### Vendors
- id
- user_id
- kitchen_name
- location
- rating

### Food Items
- id
- vendor_id
- name
- price
- description

### Orders
- id
- user_id
- vendor_id
- total_amount
- status

---

## 14. Order Flow (Important for Viva)

1. Customer selects food
2. Customer pays
3. Platform confirms payment
4. Vendor receives order
5. Delivery partner assigned
6. Order delivered

---

## 15. Minimum Features to Complete Project

- Authentication
- Vendor menu
- Customer ordering
- Payment
- Delivery integration
- Admin approval

That is enough for a complete working system.
