FROM ubuntu:latest
MAINTAINER Zhemanov Alex

EXPOSE 80 80

VOLUME "/var/www/html" 

RUN apt update #&& apt upgrade -y
RUN apt-get install nginx php7.4 php7.4-cli php7.4-fpm php7.4-json php7.4-pdo php7.4-mysql php7.4-zip php7.4-gd php7.4-mbstring php7.4-curl php7.4-xml php-pear php7.4-bcmath -y

RUN service php7.4-fpm stop
RUN service nginx stop

COPY docker.d/index.php /var/www/html/

COPY docker.d/.docker-config.sh /

CMD chmod +x /.docker-config.sh && /.docker-config.sh
