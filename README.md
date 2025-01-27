# Symfony Docker Project Setup

This repository contains a Docker-based development environment for Symfony applications.

## Prerequisites

- Docker
- Docker Compose
- Git

## Environment Setup

1. Clone this repository:
```bash
git clone git@github.com:Webanimus/symfony-dev-docker-base.git
cd symfony-dev-docker-base
```

2. Start the Docker environment:
```bash
docker compose up -d --build
```

3. Create a new Symfony project:
```bash
docker compose exec php composer create-project symfony/skeleton .
docker compose exec php composer require webapp
docker compose exec php composer require symfony/orm-pack
```

4. Set proper permissions:
```bash
docker compose exec php chown -R www-data:www-data var
```

## Accessing the Application

- Symfony application: http://localhost:8080
- phpMyAdmin: http://localhost:8081 (database management)
- MailHog: http://localhost:8025 (email testing interface)

## Database Configuration

Update your `.env` file with these database credentials:
```dotenv
DATABASE_URL="mysql://symfony:symfony@database:3306/symfony?serverVersion=mariadb-10.11.2"
```

## Docker Services

The environment includes the following services:
- **PHP (8.2-FPM)**: PHP service with all necessary extensions for Symfony
- **Nginx**: Web server
- **MariaDB (10.11.2)**: Database server
- **phpMyAdmin**: Database management tool
- **MailHog**: Email testing tool

### Database Credentials
- Database: symfony
- Username: symfony
- Password: symfony
- Root Password: root

## Common Commands

Start the environment:
```bash
docker compose up -d
```

Stop the environment:
```bash
docker compose down
```

Access PHP container:
```bash
docker compose exec php bash
```

Install Symfony dependencies:
```bash
docker compose exec php composer install
```

Clear Symfony cache:
```bash
docker compose exec php php bin/console cache:clear
```

## Development

The project directory is mounted as a volume in the PHP container. Any changes you make to your local files will be reflected immediately in the container.

## Troubleshooting

1. If you encounter permission issues:
```bash
docker compose exec php chown -R www-data:www-data var
```

2. If Composer runs out of memory:
```bash
docker compose exec php php -d memory_limit=-1 /usr/bin/composer install
```

3. To view logs:
```bash
docker compose logs -f
```
