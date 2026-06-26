# Laravel Docker Setup Collection

Dockerized boilerplates for Laravel projects. One command `make setup` to get running.

## Presets

| Preset | Stack | Default Ports |
|--------|-------|---------------|
| [laravel-mysql-setup](./laravel-mysql-setup/) | Laravel + MySQL 8.4 + Blade | Backend: `8000` |
| [laravel-postgres-setup](./laravel-postgres-setup/) | Laravel + PostgreSQL 16 + Blade | Backend: `8001` |
| [laravel-mysql-inertial-react-setup](./laravel-mysql-inertial-react-setup/) | Laravel + MySQL 8.4 + Inertia React (Breeze) | Backend: `8002`, Vite: `5174` |
| [laravel-postgres-react-setup](./laravel-postgres-react-setup/) | Laravel + PostgreSQL 16 + Inertia React (Breeze) | Backend: `8003`, Vite: `5175` |
| [laravel-postgres-nextjs-setup](./laravel-postgres-nextjs-setup/) | Laravel + PostgreSQL 16 + Next.js | Backend: `8000`, Frontend: `3000` |

All presets include **Nginx**, **Redis**, and **Mailpit** out of the box.

## Quick Start

```bash
cd <preset-directory>
make setup
```

## Commands

| Command | Description |
|---------|-------------|
| `make setup` | Full project init (first run) |
| `make up` / `make down` | Start / Stop containers |
| `make restart` / `make build` | Restart / Rebuild containers |
| `make ps` / `make logs` | Status / Logs |
| `make backend-sh` / `make db-shell` | Backend / Database CLI |
| `make migrate` / `make migrate-fresh` | Run / Reset migrations |
| `make composer-install` | Install PHP deps |
| `make frontend-sh` / `make npm-install` | Frontend CLI / Install Node deps *(frontend presets only)* |
| `make clean` | Remove everything (containers, volumes, source, .env) |

## Configuration

Edit `.env` in each preset to customize ports, project name, and database credentials. See `.env.example` for available options.
