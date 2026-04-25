# Laravel Master API

A versioned RESTful API built with Laravel demonstrating API design best practices: resource versioning, full CRUD with PUT/PATCH distinction, nested resources, Sanctum token authentication, and auto-generated API documentation via Scribe.

## Features

- **Versioned API** — all endpoints live under `/api/v1/` for clean evolution
- **Tickets System** — create and manage support tickets linked to users
- **Authors & Nested Tickets** — access tickets scoped to a specific author via nested routes
- **PUT vs PATCH** — explicit replace vs partial-update semantics on all resources
- **Sanctum Auth** — token-based authentication for all protected routes
- **Scribe Docs** — API documentation auto-generated from code annotations

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | Laravel |
| Authentication | Laravel Sanctum |
| API Docs | Scribe |
| HTTP Client | Guzzle |
| Database | MySQL |

## API Reference

All routes require `Authorization: Bearer <token>` except the login endpoint.

### Authentication

| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/login` | Get API token |

### Tickets

| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/v1/tickets` | List all tickets |
| POST | `/api/v1/tickets` | Create a ticket |
| GET | `/api/v1/tickets/{id}` | Get a ticket |
| PUT | `/api/v1/tickets/{id}` | Replace a ticket (full update) |
| PATCH | `/api/v1/tickets/{id}` | Update a ticket (partial) |
| DELETE | `/api/v1/tickets/{id}` | Delete a ticket |

### Users

| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/v1/users` | List all users |
| POST | `/api/v1/users` | Create a user |
| GET | `/api/v1/users/{id}` | Get a user |
| PUT | `/api/v1/users/{id}` | Replace a user |
| PATCH | `/api/v1/users/{id}` | Update a user |

### Authors (read-only)

| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/v1/authors` | List all authors |
| GET | `/api/v1/authors/{id}` | Get an author |

### Author Tickets (nested resource)

| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/v1/authors/{author}/tickets` | List author's tickets |
| POST | `/api/v1/authors/{author}/tickets` | Create ticket for author |
| GET | `/api/v1/authors/{author}/tickets/{ticket}` | Get specific ticket |
| PUT | `/api/v1/authors/{author}/tickets/{ticket}` | Replace ticket |
| PATCH | `/api/v1/authors/{author}/tickets/{ticket}` | Update ticket |
| DELETE | `/api/v1/authors/{author}/tickets/{ticket}` | Delete ticket |

## Project Structure

```
app/Http/Controllers/Api/
├── AuthController.php
└── V1/
    ├── ApiController.php          # Base: shared response helpers
    ├── TicketController.php
    ├── UserController.php
    ├── AuthorsController.php
    └── AuthorTicketsController.php

routes/
├── api.php       # Auth routes
└── api_v1.php    # Versioned resource routes
```

## Installation

```bash
git clone https://github.com/Ma7moud1599/Laravel_Master_Api.git
cd Laravel_Master_Api

composer install
cp .env.example .env
php artisan key:generate

# Set DB credentials in .env, then:
php artisan migrate
php artisan serve
```

### View API Docs

```bash
php artisan scribe:generate
# docs available at /docs
```

## License

MIT
