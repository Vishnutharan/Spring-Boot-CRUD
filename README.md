# Spring Boot CRUD – Employee API

A simple Spring Boot REST API that performs CRUD operations on an `Employee` entity (name, department, position, salary) stored in a MySQL database using Spring Data JPA.

## Tech stack

- Java 17
- Spring Boot 3.3.5 (Spring Web, Spring Data JPA)
- MySQL (`mysql-connector-j`), Hibernate
- Maven (Maven Wrapper included)

## Folder structure

```text
Spring-Boot-CRUD/
├── CrudApplication.CrudApplication/
│   ├── .mvn/
│   │   └── wrapper/
│   ├── src/
│   │   ├── main/
│   │   └── test/
│   ├── mvnw
│   └── pom.xml
├── .editorconfig
├── .gitignore
└── README.md
```

The Maven project lives in `CrudApplication.CrudApplication/` (package `com.demo.DemoProject`):

| Package | Purpose |
| --- | --- |
| `controller` | `EmployeeController` – REST endpoints |
| `service` | `EmployeeService` – business logic |
| `repository` | `EmployeeRepository` – Spring Data JPA repository |
| `model` | `Employee` JPA entity (table `employees`) |

## API endpoints

| Method | Path | Description |
| --- | --- | --- |
| GET | `/employees` | List all employees |
| GET | `/employees/{id}` | Get one employee |
| POST | `/employees` | Create an employee |
| PUT | `/employees/{id}` | Update an employee |
| DELETE | `/employees/{id}` | Delete an employee |

## Prerequisites

- JDK 17 or newer
- MySQL server with a database named `Employee` (or point `DB_URL` elsewhere)

## Configuration

Database settings are read from environment variables, with local defaults, in `src/main/resources/application.properties`:

| Variable | Default |
| --- | --- |
| `DB_URL` | `jdbc:mysql://localhost:3306/Employee` |
| `DB_USERNAME` | `root` |
| `DB_PASSWORD` | *(empty)* |

See `CrudApplication.CrudApplication/.env.example`. Hibernate is configured with `ddl-auto=update`, so the `employees` table is created automatically.

## Build and run

```bash
cd CrudApplication.CrudApplication
export DB_PASSWORD=your_mysql_password
./mvnw spring-boot:run          # Windows: mvnw.cmd spring-boot:run
```

The API starts on the default port `8080`, e.g. `http://localhost:8080/employees`.

To build a jar: `./mvnw package` (the tests start the Spring context and need a reachable database; use `-DskipTests` otherwise).

> **Known issue:** `pom.xml` currently has a `hibernate-core` `<dependency>` placed *outside* the `<dependencies>` block, which makes Maven reject the POM ("Malformed POM … Unrecognised tag: 'dependency'"). Move that block inside `<dependencies>` (or remove it – Spring Boot already manages Hibernate) to build the project.
