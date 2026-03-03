# Workshop: Migrate & Modernize Java Order Management System

> Using GitHub Copilot Custom Agents to systematically migrate Java 8 / Spring Boot 1.5 to Java 17+ / Spring Boot 3.x

---

## Quick Start

```bash
# 1. Clone this repository
git clone <repo-url>
cd workshop-repo

# 2. Open in VS Code
code .

# 3. Build the legacy application
cd legacy-app
mvn clean compile

# 4. Run the legacy application
mvn spring-boot:run

# 5. Test the API
curl http://localhost:8080/api/products
curl http://localhost:8080/api/orders
```

---

## What's Inside

| Folder | Purpose |
|--------|---------|
| `legacy-app/` | Legacy Java 8 / Spring Boot 1.5 Order Management System with intentional anti-patterns |

During the workshop you will create additional directories yourself:
- `modernization/` — Analysis and planning artifacts
- `agents/` — Custom Copilot agent definitions
- `src-modernized/` — Your modernized code

---

## The Legacy Application

A deliberately legacy **Order Management System** with these anti-patterns:

- **God class** (`OrderService`) handling orders, pricing, inventory, notifications, and reporting
- **Raw JDBC** with SQL string concatenation (SQL injection vulnerabilities)
- **java.util.Date** and thread-unsafe `SimpleDateFormat`
- **Manual Gson** serialization instead of Spring/Jackson
- **No dependency injection** — services create their own dependencies
- **System.out.println** instead of proper logging
- **JUnit 4** with minimal test coverage
- **Hardcoded credentials** in `DatabaseUtil`
- **No input validation** or proper error handling

---

## Workshop Guide

See [Workshop - Migrate and Modernize Java Order Management System.md](Workshop%20-%20Migrate%20and%20Modernize%20Java%20Order%20Management%20System.md) for the complete lab exercise guide.

---

## Prerequisites

| Tool | Version | Required |
|------|---------|----------|
| JDK | 17+ | Yes |
| Maven | 3.8+ | Yes |
| VS Code | Latest | Yes |
| GitHub Copilot Extension | Latest | Yes |
| GitHub Copilot Chat Extension | Latest | Yes |
| Git | 2.x+ | Yes |

---

## API Endpoints (Legacy)

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/products` | List all products |
| GET | `/api/products/{id}` | Get product by ID |
| GET | `/api/products/search?q=term` | Search products |
| GET | `/api/products/category/{category}` | Products by category |
| POST | `/api/products` | Create product |
| PUT | `/api/products/{id}/stock` | Update stock |
| GET | `/api/orders` | List all orders |
| GET | `/api/orders/{id}` | Get order by ID |
| GET | `/api/orders/status/{status}` | Orders by status |
| POST | `/api/orders` | Place new order |
| PUT | `/api/orders/{id}/status` | Update order status |
| GET | `/api/orders/{id}/summary` | Order summary (text) |
| GET | `/api/orders/report?startDate=&endDate=` | Sales report |
| DELETE | `/api/orders/{id}` | Delete order |
