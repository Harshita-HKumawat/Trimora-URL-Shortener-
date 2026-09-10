# Trimora

Trimora is a Spring Boot-based URL shortener backend with user authentication, JWT security, and basic click analytics.

## Overview

This project lets users:

- Register and log in
- Create shortened URLs
- View their own shortened links
- Track click counts and date-based analytics
- Redirect from a short URL to the original destination

It is built as a REST API using Spring Boot 3 / Java and stores data in MySQL.

## Features

- User registration and login
- JWT-based authentication
- Secure protected endpoints
- URL shortening with random 8-character short codes
- Click tracking for each shortened URL
- Analytics by date range
- Redirect endpoint for short links

## Tech Stack

- Java 26
- Spring Boot 4.1.1
- Spring Web MVC
- Spring Data JPA
- Spring Security
- MySQL
- JWT (jjwt)
- Maven

## Project Structure

```text
src/
  main/
    java/
      com/url/shortener/
        controller/
        dtos/
        models/
        repository/
        security/
        service/
    resources/
      application.properties
  test/
    java/
```

## Prerequisites

Before running the application, make sure you have:

- Java 26 installed
- Maven installed
- MySQL server running
- A MySQL database created for this project

## Database Setup

Create a MySQL database named:

```sql
CREATE DATABASE urlshortenerdb;
```

Update the database settings in `src/main/resources/application.properties` if needed:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/urlshortenerdb
spring.datasource.username=root
spring.datasource.password=your_password
spring.jpa.hibernate.ddl-auto=update
```

## Configuration

The application also includes JWT configuration:

```properties
jwt.secret=9cbe103804da070c
jwt.expiration=172800000
```

The frontend URL is configured through:

```properties
frontend.url=${FRONTEND_URL}
```

## Run the Application

From the project root, run:

### Linux / macOS

```bash
./mvnw spring-boot:run
```

### Windows

```bash
mvnw.cmd spring-boot:run
```

The API will start on:

```text
http://localhost:8080
```

## API Endpoints

### Authentication

#### Register user

```http
POST /api/auth/public/register
Content-Type: application/json
```

Request body:

```json
{
  "username": "john",
  "password": "password123",
  "email": "john@example.com"
}
```

#### Login user

```http
POST /api/auth/public/login
Content-Type: application/json
```

Request body:

```json
{
  "username": "john",
  "password": "password123"
}
```

Response includes a JWT token.

### URL operations

#### Create shortened URL

```http
POST /api/urls/shorten
Authorization: Bearer <token>
Content-Type: application/json
```

Request body:

```json
{
  "originalUrl": "https://example.com"
}
```

#### Get user's URLs

```http
GET /api/urls/myurls
Authorization: Bearer <token>
```

#### Get analytics for a URL

```http
GET /api/urls/analytics/{shortUrl}?startDate=2026-09-01T00:00:00&endDate=2026-09-30T23:59:59
Authorization: Bearer <token>
```

#### Get total clicks by date

```http
GET /api/urls/totalClicks?startDate=2026-09-01&endDate=2026-09-30
Authorization: Bearer <token>
```

#### Redirect short URL

```http
GET /{shortUrl}
```

Example:

```http
GET /QN7XOa0a
```

This redirects to the stored original URL.

## Security

The project uses Spring Security with JWT validation. Public endpoints are:

- `/api/auth/**`
- `/{shortUrl}`

Protected endpoints require authentication and a valid JWT token.

## Notes

- The generated short URLs are random 8-character strings.
- Click tracking is stored when the short link is accessed.
- The project is focused on backend functionality and can be connected to a frontend application.

## License

This project does not currently include a custom license file.

## Author

This project was created as a Java Spring Boot Trimora URL shortener example.
