FROM debian:jessie

MAINTAINER Damien QUEMARD <damien.quemard@gmail.com>

RUN apt-get update && apt-get install -y \
    nginx

# Nginx Configuration
ADD ./config/nginx.conf /etc/nginx/

# VHOSTS
RUN rm /etc/nginx/sites-enabled/default
ADD ./vhost/*.conf /etc/nginx/sites-available/
ADD ./vhost/*.conf /etc/nginx/sites-enabled/

RUN echo "upstream php-upstream { server php:9000; }" > /etc/nginx/conf.d/upstream.conf

RUN usermod -u 501 www-data
# RUN usermod -u 1000 www-data

CMD ["nginx"]

EXPOSE 80
EXPOSE 443
