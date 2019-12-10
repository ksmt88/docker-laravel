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
aws configure
```

## Service Create or Update
```bash
cd deploy
ecs-cli compose service up --aws-profile <ProfileName> --cluster <ClusterName> --launch-type FARGATE --region ap-northeast-1 --target-group-arn <arn> --container-name web --container-port 80　--timeout 10
```

### Service Delete
```bash
ecs-cli compose service down --aws-profile <ProfileName> --cluster <ClusterName>
```

## Image push
```bash
# login
$(aws ecr get-login --no-include-email --region ap-northeast-1 --profile <Profile>)

# php
docker build -t 123456789012.dkr.ecr.ap-northeast-1.amazonaws.com/sample_app_php:v1.0.0 -f ./docker/prod/php/Dockerfile .
docker push 123456789012.dkr.ecr.ap-northeast-1.amazonaws.com/sample_app_php:v1.0.0

# nginx
docker build -t 123456789012.dkr.ecr.ap-northeast-1.amazonaws.com/sample_app_nginx:v1.0.0 -f ./docker/prod/nginx/Dockerfile .
docker push 123456789012.dkr.ecr.ap-northeast-1.amazonaws.com/sample_app_nginx:v1.0.0
```

## Test
```bash
docker-compose exec php bash -c "cd /var/www/html;vendor/bin/phpunit"
```
