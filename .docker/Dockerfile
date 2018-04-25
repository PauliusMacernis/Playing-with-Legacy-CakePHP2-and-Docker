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
    && rm -f /etc/apache2/sites-available/* \
    && rm -f /etc/apache2/sites-enabled/* \
    && a2enmod rewrite

COPY .docker/httpd-foreground /usr/local/bin/
# Although the vhost.conf is the only virtual host, we name it 000-default.conf in the image
#  because we want Apache to make this the default. Apache determines the first Vhost
#  (alphabetically sorted) as the default.
COPY .docker/vhost.conf /etc/apache2/sites-available/000-default.conf
COPY . /srv/cakephp

# symlinks our Virtual Host file into the sites-enabled folder and enables the Vhost.
RUN ln -s /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-enabled/000-default.conf \
    && chmod +x /usr/local/bin/httpd-foreground
RUN chown -R www-data:www-data /srv/cakephp

WORKDIR /srv/cakephp

EXPOSE 80

# Because the http-foreground script is in the $PATH, we can reference it without the full path.
# The CMD provides defaults for an executing container, and in our case, the default is our custom bash script.
CMD ["httpd-foreground"]