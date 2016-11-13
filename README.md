# Nginx + PHP7-FPM

Entorno de desarrollo nginx con php7-fpm sobre Ubuntu 16.04 con SupervisorD

## Contiene:

- Ubuntu 16.04
- Nginx 1.11.5
- PHP 7.04 -> fpm
- Xdebug 2.4.0
- SupervisorD

## Configuración del servidor

### Nginx
server_name     app.ngnix.dev.com;
root            /usr/local/nginx/htdocs/app;
error_log       /usr/local/nginx/htdocs/app.error error;
listen  8088;

### Php
PHP CLI binary:        /usr/local/php/bin/

## Instalación

```
./build_nginx-php7-fpm_env.sh
```

## Ejecución

```
echo "127.0.0.1 app.ngnix.dev.com" >> /etc/hosts
```
```
docker run -p 8010:8088 galonso/php-fpm:7.0.4
```

http://app.ngnix.dev.com:8010/info.php
