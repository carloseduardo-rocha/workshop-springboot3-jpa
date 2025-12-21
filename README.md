# 🛒 Workshop Spring Boot 3 + JPA/Hibernate

[![Java](https://img.shields.io/badge/Java-17+-orange)](https://www.oracle.com/java/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.1.5-brightgreen)](https://spring.io/projects/spring-boot)
[![License](https://img.shields.io/badge/License-MIT-blue)](LICENSE)

Complete RESTful e-commerce API developed during Prof. Nelio Alves' course, using Spring Boot 3, JPA/Hibernate and layered architecture.

## 📌 Features

- ✅ **Complete CRUD** for Users, Products, Categories, Orders and Payments
- ✅ **JPA Associations**: @OneToMany, @ManyToMany, @OneToOne
- ✅ **Global exception handling** with `@ControllerAdvice`
- ✅ **Database**: H2 (test) + PostgreSQL (production)
- ✅ **Deployment** ready for Docker/Railway
- ✅ **Endpoints documentation** with examples

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

## 🚀 How to Run

### Prerequisites
- Java 17+
- Maven 3.8+
- Docker (optional)

### Local with H2 (test)
```bash
# Clone the project
git clone https://github.com/carloseduardo-rocha/workshop-springboot3-jpa.git

cd workshop-springboot3-jpa

# Run the application
mvn spring-boot:run -Dspring.profiles.active=test
```

Access:
- API: http://localhost:8080
- H2 Console: http://localhost:8080/h2-console
  - JDBC URL: jdbc:h2:mem:testdb
  - User: sa | Password: (empty)

### With PostgreSQL via Docker
```bash
# Start the database
docker run --name workshop-db -e POSTGRES_PASSWORD=123456 -p 5432:5432 -d postgres

# Run the application
mvn spring-boot:run -Dspring.profiles.active=dev
```

## 📚 Main Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/users` | List all users |
| POST | `/users` | Create new user |
| GET | `/orders/{id}` | Find order by ID |
| PUT | `/products/{id}` | Update product |
| GET | `/categories` | List all categories |
| DELETE | `/users/{id}` | Delete user by ID |

**Example request:**
```json
POST /users
{
  "name": "Maria Brown",
  "email": "maria@gmail.com",
  "phone": "988888888",
  "password": "123456"
}
```

## 🐳 Deployment with Docker Compose

Create a `docker-compose.yml` file:

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

And a `Dockerfile`:

```dockerfile
FROM maven:3.8.6-eclipse-temurin-17 AS build
WORKDIR /app
COPY pom.xml .
RUN mvn dependency:go-offline
COPY src ./src
RUN mvn package -DskipTests

FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
```

Run:
```bash
docker-compose up -d
```

## 🛠️ Technologies Used

- **Backend**: Spring Boot 3, Spring Data JPA, Spring Web
- **Database**: H2 (test), PostgreSQL (production)
- **Tools**: Maven, Docker, Postman
- **Patterns**: REST, Layered Architecture, Exception Handling

## 📌 Project Structure

```
src/
├── main/java/com/workshop/
│   ├── config/           # Configuration classes
│   ├── controllers/      # REST Controllers (@RestController)
│   ├── services/         # Business layer (@Service)
│   ├── repositories/     # Data access layer (@Repository)
│   ├── entities/         # JPA entities (@Entity)
│   ├── resources/        # Static resources
│   └── WorkshopApplication.java
└── test/                 # Test classes
```

## 👨‍💻 Developer

<div align="center">

<img src="https://avatars.githubusercontent.com/u/154270394?s=150" alt="Carlos Eduardo Rocha" style="border-radius: 50%; border: 3px solid #4CAF50; padding: 5px;"/>

<h3><strong>Carlos Eduardo Rocha</strong></h3>
<p>Backend Developer | Java | Spring Boot</p>

<a href="https://linkedin.com/in/carlos-eduardo-408087230">
  <img src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white"/>
</a>

<a href="https://github.com/carloseduardo-rocha">
  <img src="https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white"/>
</a>

<a href="mailto:carloseduardorocha@example.com">
  <img src="https://img.shields.io/badge/Email-D14836?style=for-the-badge&logo=gmail&logoColor=white"/>
</a>

</div>

## 📚 Based on

<div align="center">
  
**Prof. Nelio Alves Course**  
<a href="https://github.com/acenelio">
  <img src="https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white"/>
</a>
<a href="https://devsuperior.com.br">
  <img src="https://img.shields.io/badge/Website-4CAF50?style=for-the-badge&logo=google-chrome&logoColor=white"/>
</a>

</div>

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---
