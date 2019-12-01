Laravel
====

## Install
```bash
docker-compose up -d
docker-compose exec php bash -c "cd /var/www/html;composer install;cp .env.example .env;php artisan key:generate"
php artisan key:generate
```

## Test
```bash
docker-compose exec php bash -c "cd /var/www/html;vendor/bin/phpunit"
```
