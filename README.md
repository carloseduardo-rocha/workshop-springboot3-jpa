# 🛒 Workshop Spring Boot + JPA / Hibernate

[![Java](https://img.shields.io/badge/Java-17+-orange)](https://www.oracle.com/java/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.x-brightgreen)](https://spring.io/projects/spring-boot)
[![License](https://img.shields.io/badge/License-MIT-blue)](LICENSE)

Complete RESTful e-commerce API developed to consolidate backend fundamentals using **Java, Spring Boot and JPA/Hibernate**, applying layered architecture, REST principles and backend best practices.

---

## 📌 Features

* ✅ **Complete CRUD** for Users, Products, Categories, Orders and Payments
* ✅ **JPA Associations**: `@OneToMany`, `@ManyToMany`, `@OneToOne`
* ✅ **Global exception handling** with `@ControllerAdvice`
* ✅ **Database**: H2 (test) and PostgreSQL (production-ready)
* ✅ **Profiles configuration** (test / dev / prod)
* ✅ **Endpoints testing** with Postman

---

## 🏗️ Architecture

```
┌─────────────────┐
│   Controllers   │  (REST endpoints)
├─────────────────┤
│    Services     │  (Business logic)
├─────────────────┤
│   Repositories  │  (Data access)
├─────────────────┤
│   Entities      │  (JPA domain model)
└─────────────────┘
```

---

## 🚀 How to Run

### Prerequisites

* Java 17+
* Maven 3.8+
* Docker (optional)

---

### ▶️ Local execution with H2 (test profile)

```bash
git clone https://github.com/carloseduardo-rocha/workshop-springboot4-jpa.git
cd workshop-springboot4-jpa

mvn spring-boot:run -Dspring.profiles.active=test
```

Access:

* API: [http://localhost:8080](http://localhost:8080)
* H2 Console: [http://localhost:8080/h2-console](http://localhost:8080/h2-console)

  * JDBC URL: `jdbc:h2:mem:testdb`
  * User: `sa` | Password: *(empty)*

---

### ▶️ PostgreSQL with Docker (dev profile)

```bash
docker run --name workshop-db \
-e POSTGRES_PASSWORD=123456 \
-p 5432:5432 -d postgres

mvn spring-boot:run -Dspring.profiles.active=dev
```

---

## 📚 Main Endpoints

| Method | Endpoint         | Description         |
| ------ | ---------------- | ------------------- |
| GET    | `/users`         | List all users      |
| POST   | `/users`         | Create new user     |
| GET    | `/orders/{id}`   | Find order by ID    |
| PUT    | `/products/{id}` | Update product      |
| GET    | `/categories`    | List all categories |
| DELETE | `/users/{id}`    | Delete user by ID   |

### Example request

```json
POST /users
{
  "name": "Maria Brown",
  "email": "maria@gmail.com",
  "phone": "988888888",
  "password": "123456"
}
```

---

## 🐳 Docker Compose (production-ready setup)

```yaml
version: '3.8'
services:
  postgres:
    image: postgres:15
    environment:
      POSTGRES_PASSWORD: 123456
      POSTGRES_DB: workshop_db
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data
  
  app:
    build: .
    ports:
      - "8080:8080"
    environment:
      SPRING_PROFILES_ACTIVE: prod
      SPRING_DATASOURCE_URL: jdbc:postgresql://postgres:5432/workshop_db
      SPRING_DATASOURCE_USERNAME: postgres
      SPRING_DATASOURCE_PASSWORD: 123456
    depends_on:
      - postgres

volumes:
  postgres_data:
```

---

## 🛠️ Technologies Used

* **Backend**: Java, Spring Boot, Spring Data JPA, Spring Web
* **Database**: H2 (test), PostgreSQL (Intermediate)
* **Tools**: Maven, Docker, Postman
* **Patterns**: REST, Layered Architecture, Exception Handling

---

## 📌 Project Structure

```
src/
├── main/java/com/workshop/
│   ├── config/
│   ├── controllers/
│   ├── services/
│   ├── repositories/
│   ├── entities/
│   └── WorkshopApplication.java
└── test/
```

---

## 👨‍💻 Developer

**Carlos Eduardo Rocha**
Backend Developer | Java | Spring Boot

🔗 LinkedIn: [https://linkedin.com/in/carlos-eduardo-408087230](https://linkedin.com/in/carlos-eduardo-408087230)
🔗 GitHub: [https://github.com/carloseduardo-rocha](https://github.com/carloseduardo-rocha)

---

## 📚 Based on

Project inspired by **Prof. Nelio Alves** course (DevSuperior), focused on backend fundamentals and real-world Spring Boot practices.
