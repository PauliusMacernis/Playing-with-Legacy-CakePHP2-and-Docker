FROM ubuntu:12.04

LABEL maintainer="Paulius Macernis"

RUN apt-get -yqq update \
    && apt-get -yqq install \
    apache2 \
    libapache2-mod-php5 \
    php5 \
    php5-mysql \
    php5-mcrypt \
    php5-suhosin \
    && a2enmod rewrite

COPY .docker/httpd-foreground /usr/local/bin/

RUN chmod +x /usr/local/bin/httpd-foreground

EXPOSE 80

# Because the http-foreground script is in the $PATH, we can reference it without the full path.
# The CMD provides defaults for an executing container, and in our case, the default is our custom bash script.
CMD ["httpd-foreground"]