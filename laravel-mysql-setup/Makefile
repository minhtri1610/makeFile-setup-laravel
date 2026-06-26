-include .env

.PHONY: setup up down restart build ps logs logs-watch backend-sh db-shell migrate migrate-fresh composer-install clean

# Run full project initialization
setup:
	cp -n .env.example .env || true
	mkdir -p backend
	docker compose build
	docker compose run --rm backend composer create-project laravel/laravel . --prefer-dist --no-interaction || true
	docker compose up -d
	docker compose exec backend cp -n .env.example .env || true
	docker compose exec backend sed -i 's|DB_CONNECTION=sqlite|DB_CONNECTION=mysql|' .env
	docker compose exec backend sed -i 's|^# DB_HOST=.*|DB_HOST=mysql|' .env
	docker compose exec backend sed -i 's|^# DB_PORT=.*|DB_PORT=3306|' .env
	docker compose exec backend sed -i 's|^# DB_DATABASE=.*|DB_DATABASE=laravel_db|' .env
	docker compose exec backend sed -i 's|^# DB_USERNAME=.*|DB_USERNAME=laravel_user|' .env
	docker compose exec backend sed -i 's|^# DB_PASSWORD=.*|DB_PASSWORD=laravel_password|' .env
	docker compose exec backend sed -i 's|REDIS_HOST=127.0.0.1|REDIS_HOST=redis|' .env
	docker compose exec backend sed -i 's|MAIL_MAILER=log|MAIL_MAILER=smtp|' .env
	docker compose exec backend sed -i 's|MAIL_HOST=127.0.0.1|MAIL_HOST=mailpit|' .env
	docker compose exec backend sed -i 's|MAIL_PORT=2525|MAIL_PORT=1025|' .env
	sleep 10
	docker compose exec backend php artisan key:generate || true
	docker compose exec backend php artisan migrate || true

# Start containers
up:
	cp -n .env.example .env || true
	docker compose up -d

# Stop and remove containers
down:
	docker compose down

# Restart containers
restart:
	@make down
	@make up

# Rebuild docker images and start containers
build:
	docker compose up -d --build

# Show container status
ps:
	docker compose ps

# View container logs
logs:
	docker compose logs

# View container logs in real-time
logs-watch:
	docker compose logs --follow

# Terminal access to backend
backend-sh:
	docker compose exec backend sh

# CLI access to database
db-shell:
	docker compose exec mysql sh -c 'mysql -u$$MYSQL_USER -p$$MYSQL_PASSWORD $$MYSQL_DATABASE'

# Run database migrations
migrate:
	docker compose exec backend php artisan migrate

# Refresh database and run seeders
migrate-fresh:
	docker compose exec backend php artisan migrate:fresh --seed

# Install PHP dependencies
composer-install:
	docker compose exec backend composer install

# Clean up dependencies and environment files
clean:
	docker compose down -v
	rm -rf backend
	rm -f .env
