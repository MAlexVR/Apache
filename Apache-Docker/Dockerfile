#Download base image ubuntu 18.04
FROM ubuntu

#LABEL about the custom image
LABEL maintainer="mvargas.rodriguez@gmail.com"
LABEL version="1.0"
LABEL description="Imagen de prueba para el servicio \
      Apache2 y PHP."

# tzdata
ENV TZ=America/Bogota
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Apache ENVs
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_PID_FILE /var/run/apache2/apache2.pid
ENV APACHE_SERVER_NAME localhost
 
# Install services, packages and do cleanup
RUN apt-get update \
 && apt-get install -y \
    apache2 \
 && rm -rf /var/lib/apt/lists/*

# Install PHP
RUN apt-get update &&\
 apt-get install -y software-properties-common &&\
 add-apt-repository universe &&\
 apt-get install -y php7.4 libapache2-mod-php
 
# Copy files
COPY /conf/apache-conf /etc/apache2/apache2.conf
COPY index.php /var/www/html
COPY info.php /var/www/html
COPY ./bin/start.sh /start.sh

# Expose Apache
EXPOSE 80
 
# Launch Apache
RUN chmod +x /start.sh
CMD /start.sh
