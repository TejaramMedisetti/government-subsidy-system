# Backend – Spring Boot REST API

Java 21 · Spring Boot 3.2 · Spring Security (JWT) · Spring Data JPA · MySQL 8

The full project documentation (workflow, roles, API reference, setup) is in the [root README](../README.md). This file only covers what you need to work inside `backend/`.

## Run

```bash
export JWT_SECRET="$(openssl rand -hex 32)"     # required, >= 32 characters
export DB_PASSWORD='your-mysql-password'        # DB_USERNAME defaults to root
mvn spring-boot:run
```

PowerShell:

```powershell
$env:JWT_SECRET  = -join ((48..57)+(97..122) | Get-Random -Count 48 | ForEach-Object {[char]$_})
$env:DB_PASSWORD = "your-mysql-password"
mvn spring-boot:run
```

The API listens on `http://localhost:8080`. Tables are created by Hibernate on first start and demo data is seeded by `config/DataInitializer` when the database is empty.

## Test

```bash
mvn test
```

Tests use the `test` profile with an in-memory H2 database (`src/test/resources/application-test.properties`), so MySQL is not required.

## Package the application

```bash
mvn clean package
java -jar target/government-subsidy-system-1.0.0.jar
```

(The same environment variables must be set when running the jar.)

## Configuration

| Environment variable | Required | Default |
| :--- | :---: | :--- |
| `JWT_SECRET` | ✅ | – |
| `DB_PASSWORD` | | empty |
| `DB_USERNAME` | | `root` |
| `DB_URL` | | `jdbc:mysql://localhost:3306/subsidy_db?...&createDatabaseIfNotExist=true` |

See the root README for the complete property list and the security notes.
