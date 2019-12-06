FROM nginx:1.17.5-alpine

RUN mkdir -p /var/www/html/public

ADD ./docker/prod/nginx/default.conf /etc/nginx/conf.d/default.conf
ADD ./public/ /var/www/html/public/
