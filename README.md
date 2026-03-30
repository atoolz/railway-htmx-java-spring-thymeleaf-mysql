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

Use one variable per line when defining the **MySQL** plugin service (same idea as PostgreSQL’s `PGDATA` / `POSTGRES_*` block). Adjust names to match your Railway dashboard; the web app only needs **`DATABASE_URL`** pointing at **`${{MySQL.MYSQL_URL}}`**.

```bash
MYSQLDATA="" # datadir on the volume; leave empty to use the image default
MYSQLHOST="${{RAILWAY_PRIVATE_DOMAIN}}" # private hostname for other Railway services
MYSQLPORT="" # omit for default 3306, or set explicitly
MYSQLUSER="" # effective DB user (often root); emitted by the MySQL plugin
MYSQLPASSWORD="" # password for MYSQLUSER; reference the plugin’s generated secret
MYSQLDATABASE="" # database/schema name; emitted by the MySQL plugin
MYSQL_ROOT_PASSWORD="${{ secret(32, \"abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ\") }}" # bootstrap root password on first provision
MYSQL_DATABASE="" # optional first-run database name (official MySQL image)
MYSQL_USER="" # optional first-run user distinct from root
MYSQL_URL="" # canonical mysql://… for in-network clients — **web: DATABASE_URL=${{MySQL.MYSQL_URL}}**
MYSQL_PUBLIC_URL="" # mysql://… via Railway TCP proxy for external clients
DATABASE_PUBLIC_URL="${{MYSQL_PUBLIC_URL}}" # alias some tooling expects for public TCP URL
RAILWAY_TCP_PROXY_DOMAIN="" # TCP proxy host when MySQL is exposed publicly
RAILWAY_TCP_PROXY_PORT="" # TCP proxy port when public networking is enabled
RAILWAY_DEPLOYMENT_DRAINING_SECONDS="" # graceful drain window during deploys
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
