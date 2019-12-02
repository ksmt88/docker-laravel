Laravel
====

## Install
```bash
docker-compose up -d
docker-compose exec php bash -c "cd /var/www/html;composer install;cp .env.example .env;php artisan key:generate"
php artisan key:generate
```

## Credentials
```bash
ecs-cli configure profile --profile-name test_profile --access-key AKIA************** --secret-key ********************************************
ecs-cli configure --cluster <クラスター名> --default-launch-type FARGATE --region ap-northeast-1 --config-name <config名>
```

## Service Start
```bash
cd deploy
ecs-cli compose service up --ecs-profile <Profile名> --private-dns-namespace <DNSName> --enable-service-discovery --create-log-groups
```

### Service Stop
```bash
ecs-cli compose service down --ecs-profile <Profile名>
```

## Image push
```bash
# login
$(aws ecr get-login --no-include-email --region ap-northeast-1)

# php
docker build -t 698712139551.dkr.ecr.ap-northeast-1.amazonaws.com/sample_app_php:v1.0.0 ./docker/php/
docker push 698712139551.dkr.ecr.ap-northeast-1.amazonaws.com/sample_app_php:v1.0.0

# nginx
docker build -t 698712139551.dkr.ecr.ap-northeast-1.amazonaws.com/sample_app_nginx:v1.0.0 ./docker/nginx/
docker push 698712139551.dkr.ecr.ap-northeast-1.amazonaws.com/sample_app_nginx:v1.0.0
```

## Test
```bash
docker-compose exec php bash -c "cd /var/www/html;vendor/bin/phpunit"
```
