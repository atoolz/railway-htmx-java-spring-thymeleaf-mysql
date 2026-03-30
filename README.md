<p align="center">
  <img src="assets/banner.png" alt="HTMX + Spring Boot + Thymeleaf + MySQL Railway Template" width="100%">
</p>

<p align="center">
  <strong>Production-ready HTMX starter with Java, Spring Boot, Thymeleaf, and MySQL. One-click deploy to Railway.</strong>
</p>

<p align="center">
  <a href="https://railway.com/deploy/htmxspringthymeleafmysql">
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

HTMX + Spring Boot + MySQL Starter is a production-ready template for hypermedia-driven web apps. It uses HTMX for partial updates, Spring Web + Thymeleaf for server-rendered HTML, JPA + Flyway for persistence, and MySQL. **`DATABASE_URL`** must be a `mysql://user:pass@host:3306/db` string (Railway’s MySQL plugin exposes **`MYSQL_URL`** — map it on the web service). `RailwayDataSourceConfig` parses it into a HikariCP JDBC URL with SSL for non-local hosts. Tailwind and HTMX load from CDN.

### About Hosting

Multi-stage **Dockerfile** (Maven build, JRE runtime). Flyway runs migrations on startup. **`GET /health`** returns JSON and checks the database. **`PORT`** defaults to `8080`.

### Dependencies for Hosting

- Railway **MySQL** (or any compatible `mysql://` URL in `DATABASE_URL`)
- On the **web** service: `DATABASE_URL` = `${{MySQL.MYSQL_URL}}`

#### Deployment Dependencies

- [HTMX](https://htmx.org/docs/)
- [Spring Boot](https://spring.io/projects/spring-boot)
- [Thymeleaf](https://www.thymeleaf.org/)
- [Flyway](https://flywaydb.org/documentation/database/mysql)

### Why Deploy on Railway?

Railway hosts your stack with minimal configuration and scales as you grow.

<br>

## What's Inside

| Layer | Technology | Role |
|-------|-----------|------|
| **Frontend** | HTMX 2.0.7 + Tailwind (CDN) | Partial page updates |
| **Templating** | Thymeleaf | SSR + fragments for HTMX swaps |
| **API** | Spring Web | REST + HTML responses |
| **Database** | MySQL 8 + JPA + Flyway | Entities, migrations |

<br>

## Project Structure

```
.
├── src/main/java/com/atoolz/htmx/
│   ├── HtmxApplication.java
│   ├── config/RailwayDataSourceConfig.java
│   └── todo/                    # Entity, repository, controller
├── src/main/resources/
│   ├── application.yaml
│   ├── db/migration/V1__todos.sql
│   └── templates/
│       ├── home.html
│       └── fragments/todo-item.html
├── pom.xml
└── Dockerfile
```

<br>

## HTMX Patterns Demonstrated

- **`hx-post`**, **`hx-patch`**, **`hx-delete`** with `hx-target` / `hx-swap`
- **Health check** — `GET /health`

<br>

## Deploy to Railway

1. Fork this repo (or connect it)
2. New project → add **MySQL**
3. Add a **web** service from this repo (Dockerfile root)
4. Set `DATABASE_URL` = `${{MySQL.MYSQL_URL}}`
5. Health check path: **`/health`**

<br>

## Local Development

```bash
# Java 21 + Maven + local MySQL
export DATABASE_URL="mysql://root:pass@127.0.0.1:3306/htmx"
mvn spring-boot:run
```

Open [http://localhost:8080](http://localhost:8080).

<br>

## Environment Variables

| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `DATABASE_URL` | Yes | - | MySQL URL (`mysql://…`); on Railway reference `${{MySQL.MYSQL_URL}}` |
| `PORT` | No | `8080` | HTTP port |

<br>

## Railway template: MySQL service variables

Use one variable per line when defining the **MySQL** plugin service. The **web** service sets **`DATABASE_URL`** from the plugin’s **`MYSQL_URL`**. Example shape (adjust `MYSQL_DATABASE` / user; generate **`MYSQL_ROOT_PASSWORD`** with Railway’s secret helper — do not paste real passwords into the repo).

**Template icon (Railway):** [assets/icon.png](https://raw.githubusercontent.com/atoolz/railway-htmx-java-spring-thymeleaf-mysql/master/assets/icon.png) · [assets/icon.svg](https://raw.githubusercontent.com/atoolz/railway-htmx-java-spring-thymeleaf-mysql/master/assets/icon.svg)

```bash
MYSQLHOST="${{RAILWAY_PRIVATE_DOMAIN}}" # private hostname on Railway’s internal network for other services in the project
MYSQLPORT="" # leave empty for default 3306, or set an explicit port
MYSQLUSER="" # database login (often root); align with your image/plugin bootstrap user
MYSQL_URL="mysql://${{MYSQLUSER}}:${{MYSQL_ROOT_PASSWORD}}@${{RAILWAY_PRIVATE_DOMAIN}}:3306/${{MYSQL_DATABASE}}" # in-cluster mysql:// URL; web service uses ${{MySQL.MYSQL_URL}} as DATABASE_URL
MYSQLDATABASE="${{MYSQL_DATABASE}}" # plugin-style alias for the database name (no underscore)
MYSQLPASSWORD="${{MYSQL_ROOT_PASSWORD}}" # password for MYSQLUSER (typically the same as root in one-click templates)
MYSQL_DATABASE="" # logical database/schema name created on first init
MYSQL_PUBLIC_URL="mysql://${{MYSQLUSER}}:${{MYSQL_ROOT_PASSWORD}}@${{RAILWAY_TCP_PROXY_DOMAIN}}:${{RAILWAY_TCP_PROXY_PORT}}/${{MYSQL_DATABASE}}" # mysql:// via Railway TCP proxy for clients outside the private network
MYSQL_ROOT_PASSWORD="${{ secret(32, \"abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ\") }}" # generated secret at provision; never commit real values to git

# Web service (Spring Boot) — reference the MySQL plugin variable:
DATABASE_URL="${{MySQL.MYSQL_URL}}" # must be mysql://…; parsed by RailwayDataSourceConfig
```

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
