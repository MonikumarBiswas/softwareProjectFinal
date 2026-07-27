# 📚 BookVault — E-Book Management System

<div align="center">

![BookVault](https://img.shields.io/badge/BookVault-Digital%20Library-7c3aed?style=for-the-badge&logo=bookstack&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.3.5-6DB33F?style=for-the-badge&logo=springboot&logoColor=white)
![Java](https://img.shields.io/badge/Java-21-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-8.x-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![Thymeleaf](https://img.shields.io/badge/Thymeleaf-3.x-005F0F?style=for-the-badge&logo=thymeleaf&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Containerized-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Railway](https://img.shields.io/badge/Deployed%20on-Railway-0B0D0E?style=for-the-badge&logo=railway&logoColor=white)

**A fully-featured web-based digital library where users can search, read online, and download e-books.**

🌐 **Live Demo:** [softwareprojectfinal-production.up.railway.app](https://softwareprojectfinal-production.up.railway.app/)

</div>

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Design Patterns & Principles](#-design-patterns--principles)
- [Project Structure](#-project-structure)
- [Getting Started](#-getting-started)
  - [Prerequisites](#prerequisites)
  - [Local Setup](#local-setup)
  - [Docker Setup](#docker-setup)
- [Database](#-database)
- [Default Credentials](#-default-credentials)
- [API / Routes](#-api--routes)
- [Screenshots](#-screenshots)
- [Deployment](#-deployment)

---

## 🌟 Overview

**BookVault** is a full-stack E-Book Management System built as a software engineering course project. It demonstrates real-world application of classic **Design Patterns** (Singleton, Factory, Prototype, Command, Adapter, Facade) and **SOLID principles** in a production-ready Spring Boot web application.

Users can browse and search a catalog of e-books, manage a personal reading collection, and download PDFs. Admins have a dedicated panel to manage books, categories, and users.

---

## ✨ Features

### 👤 User Features
| Feature | Description |
|---------|-------------|
| 🔍 **Smart Search** | Search books by title or author from anywhere on the site |
| 📂 **Browse by Category** | Filter books by Fiction, Science, History, Technology, Bengali Literature, Liberation War, Poetry, Philosophy |
| 📖 **Read Online** | View book details and read e-books in the browser |
| 📥 **PDF Download** | Download e-books as PDF files |
| ❤️ **Personal Collection** | Save favourite books to a personal reading list |
| ↩️ **Undo Action** | Undo the last collection add/remove action |
| 🔐 **Authentication** | Secure registration and login with Spring Security |

### 🛠️ Admin Features
| Feature | Description |
|---------|-------------|
| 📚 **Book Management** | Add, edit, and delete books with cover images and PDF uploads |
| 🏷️ **Category Management** | Create and manage book categories |
| 👥 **User Management** | View and manage registered users |
| 🧩 **Quick Add from Template** | Use the Prototype pattern to pre-fill forms from book templates |
| 📦 **Import Legacy Books** | Import books from a legacy format via the Adapter pattern |

---

## 🛠 Tech Stack

| Layer | Technology |
|-------|-----------|
| **Language** | Java 21 |
| **Framework** | Spring Boot 3.3.5 |
| **Security** | Spring Security 6 |
| **Persistence** | Spring Data JPA + Hibernate |
| **Database** | MySQL 8.x |
| **Templating** | Thymeleaf 3 + Thymeleaf Spring Security Extras |
| **Validation** | Jakarta Bean Validation |
| **Build Tool** | Apache Maven 3.9 |
| **Utilities** | Lombok |
| **Containerization** | Docker (multi-stage build) |
| **Deployment** | Railway |

---

## 🎨 Design Patterns & Principles

This project explicitly demonstrates **6 design patterns** and all **5 SOLID principles**.
See [`DESIGN_PATTERNS.md`](DESIGN_PATTERNS.md) for a full mapping to source files.

### Design Patterns

| Pattern | Location | Purpose |
|---------|----------|---------|
| **Singleton** | `pattern/singleton/AuditLogger.java` | Single shared audit log for the whole app |
| **Simple Factory** | `pattern/factory/UserFactory.java` | Centralizes `User` object creation (Reader / Admin) |
| **Prototype** | `pattern/prototype/BookTemplate.java` | Clone master book templates to pre-fill the add-book form |
| **Command** | `pattern/command/` | Wraps collection add/remove as undoable command objects |
| **Adapter** | `pattern/adapter/LegacyBookAdapter.java` | Translates a legacy book record format into the app's `BookDto` |
| **Facade** | `pattern/facade/BookManagementFacade.java` | Single entry point for all admin book operations |

### SOLID Principles

| Principle | How It's Applied |
|-----------|-----------------|
| **S**ingle Responsibility | Each layer has one job — controllers, services, repositories, factories are cleanly separated |
| **O**pen/Closed | New command types or adapters can be added without editing existing code |
| **L**iskov Substitution | All `Command` implementations are fully interchangeable via the `Command` interface |
| **I**nterface Segregation | Five small, focused service interfaces instead of one large one |
| **D**ependency Inversion | Controllers/services depend on interfaces; Spring injects concrete implementations |

---

## 📁 Project Structure

```
softwareProjectFinal/
├── src/
│   └── main/
│       ├── java/com/ebookmanagement/
│       │   ├── EbookManagementSystemApplication.java   # Entry point
│       │   ├── config/                                 # Security config, DataInitializer
│       │   ├── controller/                             # Web layer (MVC controllers)
│       │   │   ├── AdminBookController.java
│       │   │   ├── AdminCategoryController.java
│       │   │   ├── AdminUserController.java
│       │   │   ├── AuthController.java
│       │   │   ├── BookController.java
│       │   │   └── UserController.java
│       │   ├── dto/                                    # Data Transfer Objects
│       │   ├── entity/                                 # JPA entities
│       │   │   ├── Book.java
│       │   │   ├── Category.java
│       │   │   ├── CollectionItem.java
│       │   │   ├── Role.java
│       │   │   └── User.java
│       │   ├── exception/                              # Custom exception classes
│       │   ├── pattern/                                # Design pattern implementations
│       │   │   ├── adapter/
│       │   │   ├── command/
│       │   │   ├── facade/
│       │   │   ├── factory/
│       │   │   ├── prototype/
│       │   │   └── singleton/
│       │   ├── repository/                             # Spring Data JPA repositories
│       │   ├── security/                               # Custom UserDetailsService
│       │   └── service/                                # Business logic interfaces + impls
│       └── resources/
│           ├── templates/                              # Thymeleaf HTML templates
│           ├── static/                                 # CSS, JS, images
│           └── application.properties                  # App configuration
├── uploads/                                            # Uploaded PDFs and cover images
├── database-setup.sql                                  # Reference SQL script
├── Dockerfile                                          # Multi-stage Docker build
├── pom.xml                                             # Maven dependencies
└── DESIGN_PATTERNS.md                                  # Pattern documentation
```

---

## 🚀 Getting Started

### Prerequisites

- **Java 21** (JDK) — [Download](https://adoptium.net/)
- **Maven 3.9+** — [Download](https://maven.apache.org/download.cgi)
- **MySQL 8.x** — [Download](https://dev.mysql.com/downloads/)
- *(Optional)* **Docker** — [Download](https://www.docker.com/products/docker-desktop/)

### Local Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/your-username/softwareProjectFinal.git
   cd softwareProjectFinal
   ```

2. **Create the database**
   ```sql
   CREATE DATABASE IF NOT EXISTS ebook_management_system
       CHARACTER SET utf8mb4
       COLLATE utf8mb4_unicode_ci;
   ```
   > Tables are auto-created by Hibernate on first run. The default admin and seed categories are inserted automatically by `DataInitializer`.

3. **Configure database credentials**

   Edit `src/main/resources/application.properties`:
   ```properties
   spring.datasource.url=jdbc:mysql://localhost:3306/ebook_management_system?createDatabaseIfNotExist=true&useSSL=false&serverTimezone=UTC
   spring.datasource.username=YOUR_MYSQL_USERNAME
   spring.datasource.password=YOUR_MYSQL_PASSWORD
   ```

4. **Build and run**
   ```bash
   mvn spring-boot:run
   ```

5. **Open in your browser**
   ```
   http://localhost:8080
   ```

### Docker Setup

1. **Build the Docker image**
   ```bash
   docker build -t bookvault .
   ```

2. **Run the container**
   ```bash
   docker run -p 8080:8080 \
     -e SPRING_DATASOURCE_URL=jdbc:mysql://<your-mysql-host>:3306/ebook_management_system \
     -e SPRING_DATASOURCE_USERNAME=<username> \
     -e SPRING_DATASOURCE_PASSWORD=<password> \
     bookvault
   ```

3. **Open in your browser**
   ```
   http://localhost:8080
   ```

---

## 🗄 Database

The database schema is managed automatically by **Hibernate JPA** (`ddl-auto=update`).

**Tables created automatically:**

| Table | Description |
|-------|-------------|
| `users` | Registered users with roles |
| `categories` | Book categories |
| `books` | E-book catalog with metadata and file paths |
| `collection_items` | Many-to-many mapping of users ↔ saved books |

A reference SQL script is included at [`database-setup.sql`](database-setup.sql).

---

## 🔑 Default Credentials

> These are seeded automatically on first run by `DataInitializer`.

| Role | Email | Password |
|------|-------|----------|
| **Admin** | `admin@ebook.com` | `admin123` |

Register a new account at `/register` for normal user access.

---

## 🗺 API / Routes

### Public Routes
| Method | Path | Description |
|--------|------|-------------|
| `GET` | `/` | Homepage with hero search & latest books |
| `GET` | `/books` | Browse all books (supports `?search=` and `?category=`) |
| `GET` | `/books/{id}` | Book detail page |
| `GET` | `/login` | Login page |
| `POST` | `/login` | Authenticate |
| `GET` | `/register` | Registration page |
| `POST` | `/register` | Create a new user account |

### User Routes (Authenticated)
| Method | Path | Description |
|--------|------|-------------|
| `GET` | `/collection` | View personal collection |
| `POST` | `/collection/add/{bookId}` | Add a book to collection |
| `POST` | `/collection/remove/{bookId}` | Remove a book from collection |
| `POST` | `/collection/undo` | Undo the last collection action |
| `GET` | `/books/{id}/download` | Download a book's PDF |

### Admin Routes (Role: ADMIN)
| Method | Path | Description |
|--------|------|-------------|
| `GET` | `/admin/books` | Manage all books |
| `GET` | `/admin/books/add` | Add new book form |
| `POST` | `/admin/books/add` | Submit new book |
| `GET` | `/admin/books/edit/{id}` | Edit book form |
| `POST` | `/admin/books/edit/{id}` | Submit book edits |
| `POST` | `/admin/books/delete/{id}` | Delete a book |
| `GET` | `/admin/books/add-from-template/{key}` | Pre-fill form using Prototype pattern |
| `POST` | `/admin/books/import-legacy` | Import via Adapter pattern |
| `GET` | `/admin/categories` | Manage categories |
| `GET` | `/admin/users` | View all users |

---

## 📸 Screenshots

<table>
  <tr>
    <td align="center"><b>🏠 Homepage</b></td>
    <td align="center"><b>📚 Browse Books</b></td>
  </tr>
  <tr>
    <td>Hero search, category chips, latest books showcase</td>
    <td>Full catalog with search and category filter</td>
  </tr>
  <tr>
    <td align="center"><b>📖 Book Details</b></td>
    <td align="center"><b>🔐 Login / Register</b></td>
  </tr>
  <tr>
    <td>Book metadata, read online, download PDF, save to collection</td>
    <td>Secure authentication forms with password toggle</td>
  </tr>
</table>

---

## 🚢 Deployment

This project is deployed on **Railway** using the included `Dockerfile`.

**Environment variables required on Railway:**

| Variable | Description |
|----------|-------------|
| `SPRING_DATASOURCE_URL` | Full JDBC URL for the MySQL database |
| `SPRING_DATASOURCE_USERNAME` | Database username |
| `SPRING_DATASOURCE_PASSWORD` | Database password |
| `PORT` | Injected automatically by Railway |

The Docker container uses a **multi-stage build** to keep the final image lean:
- **Stage 1** — Builds the JAR with Maven (Eclipse Temurin 21 + Alpine)
- **Stage 2** — Runs the JAR with a minimal JRE image (Eclipse Temurin 21 JRE Alpine)

JVM memory is limited to `-Xmx400m -Xms200m` to fit within Railway's free tier.

---

## 📄 License

This project was created for academic purposes as a Software Engineering course final project.

---

<div align="center">

**Built with ❤️ & Spring Boot** | © 2025 E-Book Management System

</div>
