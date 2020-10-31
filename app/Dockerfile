FROM debian:buster

RUN apt update
RUN apt install apache2 -y

# DEBUG DELETE LATER
RUN apt install -y vim less net-tools

# Enable modules for FCGI
RUN a2enmod proxy_fcgi

RUN mkdir /app
RUN chown www-data:www-data /app

COPY src /app

COPY conf/vhosts /etc/apache2/conf-enabled

EXPOSE 80/TCP

CMD service apache2 start && tail -f /app/access.log /app/error.log
