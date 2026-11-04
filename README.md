# Library REST API — IN3101 Lab 02

A Spring Boot RESTful CRUD API connected to MySQL for managing books, built for **IN3101 – Enterprise Application Development (Lab Sheet 02)** at the Faculty of Information Technology, University of Moratuwa.

## Student Information

- **Name:** Agnes Ostina
- **Index Number:** `235085H`
- **Module:** IN3101 – Enterprise Application Development (Level 3 Semester 1)
- **Lab:** Lab Sheet 02 – Building a REST API with Spring Boot

---

## Tech Stack

- **Java:** JDK 21
- **Framework:** Spring Boot 4.1.2 (WebMVC, Spring Data JPA, Jakarta Bean Validation)
- **Database:** MySQL 8 (`library_db`)
- **API Documentation:** SpringDoc OpenAPI / Swagger UI (`3.1.1`)
- **Build Tool:** Apache Maven (Maven Wrapper included)

---

## Project Structure

```text
library-api/
├── src/main/java/lk/ac/mrt/fit/library_api/
│   ├── LibraryApiApplication.java       # Main Spring Boot entry point
│   ├── model/Book.java                  # JPA Entity with Bean Validation
│   ├── repository/BookRepository.java   # Spring Data JPA Repository
│   ├── service/BookService.java         # Business logic layer
│   └── controller/BookController.java   # REST Controller + Swagger annotations
├── src/main/resources/
│   └── application.properties           # MySQL & Hibernate configuration
├── Library_API.postman_collection.json  # Postman collection for endpoint testing
└── pom.xml                              # Maven dependencies & build configuration
```

---

## Getting Started

### 1. Create the MySQL Database

Open MySQL Workbench (or MySQL CLI) and run:

```sql
DROP DATABASE IF EXISTS library_db;
CREATE DATABASE library_db;
```

### 2. Configure Database Password & Run the Application

The project reads the MySQL `root` password from the `DB_PASSWORD` environment variable (`src/main/resources/application.properties`).

**Windows (PowerShell):**
```powershell
$env:DB_PASSWORD='your_mysql_root_password'
.\mvnw.cmd spring-boot:run
```

**macOS / Linux:**
```bash
export DB_PASSWORD='your_mysql_root_password'
./mvnw spring-boot:run
```

The server starts on `http://localhost:8080` and Hibernate automatically creates/updates the `book` table.

---

## REST API Endpoints

Base URL: `http://localhost:8080/api/books`

| Method | Endpoint | Action | Success Status | Error Status |
| :--- | :--- | :--- | :--- | :--- |
| `GET` | `/api/books` | List all books | `200 OK` | — |
| `GET` | `/api/books/{id}` | Get a book by ID | `200 OK` | `404 Not Found` |
| `POST` | `/api/books` | Create a new book | `201 Created` | `400 Bad Request` |
| `PUT` | `/api/books/{id}` | Update an existing book | `200 OK` | `400 Bad Request` / `404 Not Found` |
| `DELETE` | `/api/books/{id}` | Delete a book by ID | `204 No Content` | `404 Not Found` |

### Sample Request Body (`POST` / `PUT`)

```json
{
  "title": "235085H - Clean Code",
  "author": "Robert C. Martin",
  "isbn": "9780132350884",
  "price": 4500.00
}
```

---

## API Documentation & Testing

- **Swagger UI:** `http://localhost:8080/swagger-ui.html`
- **OpenAPI JSON Spec:** `http://localhost:8080/v3/api-docs`
- **Postman:** Import `Library_API.postman_collection.json` into Postman to test all CRUD and validation scenarios (`S1`–`S7`).
