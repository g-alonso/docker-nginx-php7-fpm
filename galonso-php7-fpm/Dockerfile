# docker build -t galonso/php-fpm:7.0.4 .

FROM       galonso/nginx:1.11.5
MAINTAINER Gabriel Alonso <gbr.alonso@gmail.com>

RUN sudo apt-get update -qq -y
RUN sudo apt-get install -qq -y \
    libcurl4-openssl-dev        \
    libmysqlclient-dev          \
    libpq-dev                   \
    libvpx-dev                  \
    libjpeg-dev                 \
    libpng-dev                  \
    libmcrypt-dev               \
    libcurl4-openssl-dev        \
    pkg-config

RUN cd /tmp;                                                      \
    curl -LO http://php.net/distributions/php-7.0.4.tar.bz2;      \
    tar xvjf *.tar.bz2; rm -f *.tar.bz2;                          \
    cd php-*;                                                     \
    ./configure                                                   \
      --prefix=/usr/local/php                                     \
      --with-openssl                         \
      --with-config-file-path=/usr/local/php                      \
      --with-config-file-scan-dir=/usr/local/php/php.ini.d/       \
      --with-curl                                                 \
      --enable-pcntl                                              \
      --with-readline                                             \
      --enable-soap                                               \
      --enable-sockets                                            \
      --enable-zip                                                \
      --with-zlib                                                 \
      --with-bz2                                                  \
      --with-gettext                                              \
      --with-mhash                                                \
      --with-mysql                                                \
      --with-mysqli                                               \
      --with-pdo-mysql                                            \
      --with-pgsql                                                \
      --with-pdo-pgsql                                            \
      --enable-mbstring                                           \
      --with-xmlrpc                                               \
      --with-gd                                                   \
      --with-mcrypt                                               \
      --enable-fpm                                                \
      ;                                                           \
    make && make install;                                         \
    cp php.ini-development /usr/local/php/php.ini;                \
    cd; rm -rf /tmp/php-*

ENV PATH "$PATH:/usr/local/php/bin"

# Instalamos XDEBUG
RUN cd /tmp;                                                      \
    wget -c "http://xdebug.org/files/xdebug-2.4.0.tgz";           \
    tar -xf xdebug-2.4.0.tgz;                                     \
    cd xdebug-2.4.0/;                                             \
    /usr/local/php/bin/phpize;                                    \
    ./configure                                                   \
      --with-php-config=/usr/local/php/bin/php-config             \
    ;                                                             \
    make && make install;                                         \
    echo "zend_extension=xdebug.so" >> /usr/local/php/php.ini;

# Agregamos nginx server y root folder
ADD ./default.conf /usr/local/nginx/conf.d/default.conf
ADD ./app /usr/local/nginx/htdocs/app

# Agregamos nuestra configuracion para supervisord
ADD supervisord.conf /etc/supervisord.conf

RUN sudo chgrp default /usr/local/nginx/htdocs/ -R
RUN sudo chown default /usr/local/nginx/htdocs/ -R

CMD ["/usr/bin/supervisord", "-n", "-c",  "/etc/supervisord.conf"]
