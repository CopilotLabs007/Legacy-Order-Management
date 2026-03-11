# Legacy Order Management System

A legacy Java 8 / Spring Boot 1.5 order management application using Spring JDBC and an H2 in-memory database. The app exposes a REST API for managing products and orders, along with a simple HTML/JS product-listing UI.

---

## Table of Contents

- [Tech Stack](#tech-stack)
- [Prerequisites](#prerequisites)
- [Repository Structure](#repository-structure)
- [Build](#build)
- [Run](#run)
- [Application URLs](#application-urls)
  - [UI](#ui)
  - [Product API](#product-api)
  - [Order API](#order-api)
- [Java Upgrade Guide](#java-upgrade-guide)
- [License](#license)

---

## Tech Stack

| Component         | Version          |
|-------------------|------------------|
| Java              | 8 (source level) |
| Spring Boot       | 1.5.22.RELEASE   |
| Spring JDBC       | Raw JDBC, no ORM |
| Database          | H2 (in-memory)   |
| JSON              | Gson 2.8.5       |
| Utilities         | Commons Lang 2.6 |
| Logging           | Log4j 1.2        |
| Testing           | JUnit 4          |
| Build tool        | Maven 3.9+       |

---

## Prerequisites

| Tool  | Version  | Notes |
|-------|----------|-------|
| Java  | 8 or 25  | Java 8 is the source-compatibility target; Java 25 works with the JVM flags shown below |
| Maven | 3.9+     | Used for building and running the application |

> **Tip (macOS / Homebrew):** If you are using OpenJDK 25, set `JAVA_HOME` before running any Maven or Java commands:
> ```bash
> export JAVA_HOME=/opt/homebrew/Cellar/openjdk/25.0.2/libexec/openjdk.jdk/Contents/Home
> ```

---

## Repository Structure

```
Legacy-Order-Management/
├── java-app-modernization/
│   ├── legacy-app/              # Main Spring Boot application
│   │   ├── src/
│   │   │   ├── main/            # Application source code
│   │   │   └── test/            # Unit tests
│   │   ├── pom.xml              # Maven build descriptor
│   │   └── README.md            # Detailed app-level documentation
│   ├── Images/                  # Screenshots used in upgrade guide
│   └── README Java Upgrade.md   # Java upgrade walkthrough
├── LICENSE
└── README.md                    # This file
```

---

## Build

```bash
cd java-app-modernization/legacy-app
mvn clean package -DskipTests
```

A successful build produces `target/order-management-1.0.0.jar`.

---

## Run

### Option 1 – Maven (Java 8 / Java 11 / Java 17)

```bash
cd java-app-modernization/legacy-app
mvn spring-boot:run -Dmaven.test.skip=true
```

### Option 2 – JAR (Java 25)

Spring Boot 1.5 requires additional `--add-opens` flags on newer JVMs:

```bash
cd java-app-modernization/legacy-app
$JAVA_HOME/bin/java \
  --add-opens java.base/java.lang=ALL-UNNAMED \
  --add-opens java.base/java.io=ALL-UNNAMED \
  --add-opens java.base/java.util=ALL-UNNAMED \
  --add-opens java.base/java.lang.reflect=ALL-UNNAMED \
  --add-opens java.base/java.text=ALL-UNNAMED \
  --add-opens java.desktop/java.awt.font=ALL-UNNAMED \
  -jar target/order-management-1.0.0.jar
```

The application starts on **port 8080** by default.

---

## Application URLs

### UI

| Page                | URL                              |
|---------------------|----------------------------------|
| Product Listing     | http://localhost:8080            |
| H2 Database Console | http://localhost:8080/h2-console |

> **H2 Console credentials** (default):
>
> | Field      | Value                |
> |------------|----------------------|
> | JDBC URL   | `jdbc:h2:mem:orderdb` |
> | User Name  | `sa`                 |
> | Password   | *(leave blank)*      |

### Product API

| Method | URL                                                    | Description           |
|--------|--------------------------------------------------------|-----------------------|
| GET    | http://localhost:8080/api/products                     | List all products     |
| GET    | http://localhost:8080/api/products/{id}                | Get product by ID     |
| GET    | http://localhost:8080/api/products/search?q={term}     | Search products       |
| GET    | http://localhost:8080/api/products/category/{category} | Products by category  |
| POST   | http://localhost:8080/api/products                     | Create a product      |
| PUT    | http://localhost:8080/api/products/{id}/stock          | Update stock quantity |

### Order API

| Method | URL                                                                             | Description          |
|--------|---------------------------------------------------------------------------------|----------------------|
| GET    | http://localhost:8080/api/orders                                                | List all orders      |
| GET    | http://localhost:8080/api/orders/{id}                                           | Get order by ID      |
| GET    | http://localhost:8080/api/orders/status/{status}                                | Orders by status     |
| POST   | http://localhost:8080/api/orders                                                | Place an order       |
| PUT    | http://localhost:8080/api/orders/{id}/status                                    | Update order status  |
| GET    | http://localhost:8080/api/orders/{id}/summary                                   | Order summary (text) |
| GET    | http://localhost:8080/api/orders/report?startDate=yyyy-MM-dd&endDate=yyyy-MM-dd | Sales report         |
| DELETE | http://localhost:8080/api/orders/{id}                                           | Delete an order      |

---

## Java Upgrade Guide

See [`java-app-modernization/README Java Upgrade.md`](java-app-modernization/README%20Java%20Upgrade.md) for step-by-step instructions on upgrading this application to Java 21 using **GitHub Copilot App Modernization – Upgrade for Java**.

Additional reference: [GitHub Copilot App Modernization – Upgrade for Java (Microsoft Learn)](https://learn.microsoft.com/en-us/java/upgrade/overview)

---

## License

This project is licensed under the [MIT License](LICENSE).
