# Legacy Order Management System

A legacy Java 8 / Spring Boot 1.5 order management application using JDBC and H2 in-memory database.

## Prerequisites

- **Java**: OpenJDK 25 (installed via Homebrew)
- **Maven**: 3.9+ (installed via Homebrew)

Set `JAVA_HOME` before running Maven or Java commands:

```bash
export JAVA_HOME=/opt/homebrew/Cellar/openjdk/25.0.2/libexec/openjdk.jdk/Contents/Home
```

## Build

```bash
cd java-app-modernization/legacy-app
mvn clean package -DskipTests
```

## Run

Since Spring Boot 1.5 requires additional JVM flags on Java 25:

```bash
$JAVA_HOME/bin/java \
  --add-opens java.base/java.lang=ALL-UNNAMED \
  --add-opens java.base/java.io=ALL-UNNAMED \
  --add-opens java.base/java.util=ALL-UNNAMED \
  --add-opens java.base/java.lang.reflect=ALL-UNNAMED \
  --add-opens java.base/java.text=ALL-UNNAMED \
  --add-opens java.desktop/java.awt.font=ALL-UNNAMED \
  -jar target/order-management-1.0.0.jar
```

The app starts on **port 8080**.

## URLs

### UI

| Page | URL |
|------|-----|
| Product Listing | http://localhost:8080 |
| H2 Database Console | http://localhost:8080/h2-console |

### Product API

| Method | URL | Description |
|--------|-----|-------------|
| GET | http://localhost:8080/api/products | List all products |
| GET | http://localhost:8080/api/products/{id} | Get product by ID |
| GET | http://localhost:8080/api/products/search?q={term} | Search products |
| GET | http://localhost:8080/api/products/category/{category} | Products by category |
| POST | http://localhost:8080/api/products | Create a product |
| PUT | http://localhost:8080/api/products/{id}/stock | Update stock |

### Order API

| Method | URL | Description |
|--------|-----|-------------|
| GET | http://localhost:8080/api/orders | List all orders |
| GET | http://localhost:8080/api/orders/{id} | Get order by ID |
| GET | http://localhost:8080/api/orders/status/{status} | Orders by status |
| POST | http://localhost:8080/api/orders | Place an order |
| PUT | http://localhost:8080/api/orders/{id}/status | Update order status |
| GET | http://localhost:8080/api/orders/{id}/summary | Order summary (text) |
| GET | http://localhost:8080/api/orders/report?startDate=yyyy-MM-dd&endDate=yyyy-MM-dd | Sales report |
| DELETE | http://localhost:8080/api/orders/{id} | Delete an order |

## Tech Stack

- Java 8 (source level)
- Spring Boot 1.5.22
- Spring JDBC (raw JDBC, no ORM)
- H2 in-memory database
- Gson for JSON serialization
- Commons Lang 2.6
- Log4j 1.2
- JUnit 4
