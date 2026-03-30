<p align="center">
  <img src="assets/banner.png" alt="HTMX + Spring Boot + Thymeleaf + MySQL Railway Template" width="100%">
</p>

<p align="center">
  <strong>Production-ready HTMX starter with Java, Spring Boot, Thymeleaf, and MySQL. One-click deploy to Railway.</strong>
</p>

<p align="center">
  <a href="https://railway.com/deploy/htmx-spring-thymeleaf-mysql">
    <img src="https://railway.com/button.svg" alt="Deploy on Railway">
  </a>
</p>

<p align="center">
  <a href="https://github.com/atoolz/railway-htmx-java-spring-thymeleaf-mysql/blob/master/LICENSE">
    <img src="https://img.shields.io/github/license/atoolz/railway-htmx-java-spring-thymeleaf-mysql?style=flat-square&color=00c9a7" alt="License">
  </a>
  <img src="https://img.shields.io/badge/Java-21-ED8B00?style=flat-square" alt="Java 21">
  <img src="https://img.shields.io/badge/Spring%20Boot-3.4-6DB33F?style=flat-square" alt="Spring Boot">
  <img src="https://img.shields.io/badge/HTMX-2.0.7-3366CC?style=flat-square" alt="HTMX 2.0.7">
  <img src="https://img.shields.io/badge/MySQL-8-4479A1?style=flat-square" alt="MySQL">
</p>

<br>

## Deploy and Host HTMX + Spring Boot + MySQL Starter on Railway

Same architecture as the PostgreSQL variant: HTMX + Thymeleaf + JPA + Flyway, with **`DATABASE_URL`** shaped like `mysql://user:pass@host:3306/db` (Railway MySQL). SSL mode is applied for remote hosts.

### Dependencies for Hosting

- Railway **MySQL** (or compatible `DATABASE_URL`)
- `DATABASE_URL` on the web service (reference your MySQL plugin variable)

#### Deployment Dependencies

- [HTMX](https://htmx.org/docs/)
- [Spring Boot](https://spring.io/projects/spring-boot)
- [Thymeleaf](https://www.thymeleaf.org/)
- [Flyway](https://flywaydb.org/)

<br>

## What's Inside

| Layer | Technology | Role |
|-------|-----------|------|
| **Frontend** | HTMX + Tailwind (CDN) | Partial updates |
| **Templating** | Thymeleaf | SSR + fragments |
| **Database** | MySQL + JPA + Flyway | Todo schema |

<br>

## Deploy to Railway

1. Add **MySQL** + web service from this repo
2. Set **`DATABASE_URL`** to your MySQL connection string
3. Health check: **`GET /health`**

<br>

## Local Development

```bash
export DATABASE_URL="mysql://root:pass@127.0.0.1:3306/htmx"
mvn spring-boot:run
```

<br>

## Environment Variables

| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `DATABASE_URL` | Yes | - | MySQL URL (`mysql://…`) |
| `PORT` | No | `8080` | HTTP port |

<br>

## Part of the HTMX Railway Collection

This is one of 15 HTMX starter templates covering different backend stacks, all following the same pattern and ready for Railway deployment:

| Stack | Status |
|-------|--------|
| Bun + Elysia | Coming soon |
| .NET + Razor | Coming soon |
| Elixir + Phoenix | Coming soon |
| Go + Chi | [Live](https://github.com/atoolz/railway-htmx-go-templ-chi-pg) |
| Go + Echo | [Live](https://github.com/atoolz/railway-htmx-go-templ-echo-pg) |
| Go + Fiber | [Live](https://github.com/atoolz/railway-htmx-go-templ-fiber-pg) |
| **Java + Spring Boot (MySQL)** | **This repo** |
| Java + Spring Boot (PostgreSQL) | [Live](https://github.com/atoolz/railway-htmx-java-spring-thymeleaf-pg) |
| Node + Express | [Live](https://github.com/atoolz/railway-htmx-node-express-ejs-pg) |
| Node + Hono | [Live](https://github.com/atoolz/railway-htmx-node-hono-jsx-pg) |
| PHP + Laravel | [Live](https://github.com/atoolz/railway-htmx-php-laravel-mysql) |
| Python + Django | [Live](https://github.com/atoolz/railway-htmx-python-django-pg) |
| Python + FastAPI | [Live](https://github.com/atoolz/railway-htmx-python-fastapi-jinja2-pg) |
| Ruby + Rails 8 | [Live](https://github.com/atoolz/railway-htmx-ruby-rails8-pg) |
| Rust + Axum + Askama | [Live](https://github.com/atoolz/railway-htmx-rust-axum-askama-pg) |

<br>

## License

[MIT](LICENSE)

---

<p align="center">
  <sub>Built by <a href="https://github.com/atoolz">AToolZ</a> for the HTMX community</sub>
</p>
