# ☕ Teahouse

## Overview

Teahouse is a **full-stack web application** designed to streamline tea shop operations by decoupling customer-facing ordering from internal inventory management.

**The Problem:** Tea shops typically juggle manual order-taking and disconnected inventory tracking, leading to overselling, stock-outs, and lost sales visibility.

**The Solution:** Teahouse separates customer-facing ordering (browsing menu, placing orders, tracking confirmations) from internal operations (real-time stock tracking, inventory updates, fulfillment management). Built with Spring Boot and a relational database backend, it ensures accurate stock visibility across both channels and prevents overselling through transactional consistency.

## Features

**Customer Ordering**
- Browse tea menu with real-time stock availability and pricing
- Add items to cart, apply promotions, and complete secure checkout
- Receive order confirmation and estimated fulfillment time
- View past orders and reorder frequently purchased items

**Admin Inventory Management**
- Live dashboard showing current stock levels by product
- Automatic low-stock alerts and reorder reminders
- Transactional inventory updates as orders are fulfilled
- Audit trail of all inventory changes for compliance and troubleshooting
- Product catalog management (add, update, retire items)

## Technical Stack

| Layer | Technology |
|-------|-----------|
| **Backend** | Java 11+, Spring Boot, Spring Data JPA |
| **Frontend** | HTML5, CSS3, JavaScript (vanilla or framework if applicable) |
| **Database** | MySQL / PostgreSQL |
| **Build Tool** | Maven / Gradle |
| **API** | RESTful JSON endpoints |

## Architecture & How It Works

**Request Flow (Customer Places Order):**
1. Customer selects tea products on frontend → HTTP POST to `/api/orders`
2. Spring Boot backend validates:
   - Product exists and is active
   - Requested quantity ≤ available stock
3. Database transaction:
   - Creates `Order` record with customer details
   - Decrements `Product.availableStock`
4. Returns order confirmation JSON to frontend
5. Admin sees live inventory update on dashboard

**Admin Inventory Update Flow:**
1. Admin updates stock on dashboard → PUT to `/api/inventory/{productId}`
2. Backend persists changes to database
3. Frontend reflects live inventory updates for customers

**Why This Architecture:**
- **Spring Boot** provides rapid REST API development and transaction management
- **Relational Database** ensures ACID compliance for inventory consistency (prevents overselling)
- **Vanilla JavaScript Frontend** keeps deployment lightweight and responsive

## Getting Started

### Prerequisites
- Java 11+ installed
- Maven (or Gradle)
- MySQL or PostgreSQL database (running locally or in Docker)

### Installation & Running

1. **Clone the repository**
   ```bash
   git clone https://github.com/rhaubenstock/Teahouse.git
   cd Teahouse

2. Configure database connection: update src/main/resources/application.properties with your database credentials

3. Build and run the backend
   ```bash
   mvn clean install
   mvn spring-boot:run
   
_(or use ./gradlew bootRun if Gradle)_
   
4. Access the application

Open http://localhost:8080 in your browser for the customer portal
Admin dashboard accessible at /admin (if applicable)

## Future Enhancements

- Order confirmation notifications (email/SMS)
- Analytics dashboard for sales and inventory trends
- Payment gateway integration (e.g., Stripe/PayPal)
