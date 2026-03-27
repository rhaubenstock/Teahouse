# ☕ Teahouse

## Overview

Teahouse is a full-stack web application that manages both **customer-facing order placement** and **internal inventory management** for a tea shop.

## Features

### Customer Interface
- Browse and place tea orders

### Admin/Inventory Interface
- Stock level monitoring

## Technical Stack

**Backend:**
- SpringBoot

**Frontend:**
- HTML/CSS/JavaScript

## Setup Instructions

### Requirements

- Java 17 or higher
- MySQL
- Maven (or use the included `mvnw` wrapper)

### 1. Run the Application
In one console run the Spring Boot backend:
```
./mvnw spring-boot:run
```
Maven will download dependencies and start the application on http://localhost:8080.


## Project Architecture Diagram

```mermaid
flowchart TD
    U[User / Admin Browser] -->|HTTP Requests| C[Spring MVC Controllers\ncontrollers/*]

    C --> V[Thymeleaf Templates\ntemplates/*.html]
    C --> S[Service Layer\nservice/*]

    S --> D[Domain Models\ndomain/*\nProduct, Part, InhousePart, OutsourcedPart]
    S --> VAL[Validation Layer\nvalidators/*]
    S --> R[Spring Data Repositories*]

    R --> DB[(Database/n JPA persistence)]

    B[Application Startup\nDemoApplication + BootStrapData] --> S
    B --> R

    ST[Static Assets\nstatic/index.html + static/css/demo.css] --> U
```

## Project ER Diagram

```mermaid
erDiagram
    PRODUCT {
        long id PK
        string name
        double price
        int inv
    }

    PART {
        long id PK
        string name
        double price
        int inv
        int minInv
        int maxInv
        int part_type
    }

    INHOUSE_PART {
        int partId
    }

    OUTSOURCED_PART {
        string companyName
    }

    PRODUCT_PART {
        long product_id FK
        long part_id FK
    }

    PRODUCT_PART }o--|| PRODUCT : links
    PRODUCT_PART }o--|| PART : links
    PART ||--o| INHOUSE_PART : subtype
    PART ||--o| OUTSOURCED_PART : subtype
```

## Example Screenshots
### Main Page
![Main Page](./images/teahouse_homepage.png.png)
### Add Product Form
![Update Insourced Product Form](./images/update_insourced.png.png)
### Modify Product Form
![Updated Outsourced Form](./images/update_outsourced.png.png)