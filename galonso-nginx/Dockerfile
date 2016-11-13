#docker build -t galonso/nginx:1.11.5 .

FROM       galonso/ubuntu:16.04
MAINTAINER Gabriel Alonso <gbr.alonso@gmail.com>

RUN sudo apt-get install -y libpcre3 libpcre3-dev
RUN curl -LO http://nginx.org/download/nginx-1.11.5.tar.gz
RUN tar xvf nginx-1.11.5.tar.gz

USER default

RUN cd nginx-1.11.5;                      \
 ./configure                              \
    --user=default                          \
    --group=default                         \
    --prefix=/usr/local/nginx                   \
    --sbin-path=/usr/local/nginx           \
    --conf-path=/usr/local/nginx/nginx.conf     \
    --pid-path=/usr/local/nginx/run/nginx.pid         \
    --lock-path=/usr/local/nginx/run/nginx.lock       \
    --error-log-path=/usr/local/nginx/log/error.log \
    --http-log-path=/usr/local/nginx/log/access.log \
    --with-http_gzip_static_module        \
    --with-http_stub_status_module        \
    --with-http_ssl_module                \
    --with-pcre                           \
    --with-file-aio                       \
    --with-http_realip_module             \
    --without-http_scgi_module            \
    --without-http_uwsgi_module           ; \
    make && make install;

ADD ./nginx.conf /usr/local/nginx/nginx.conf
RUN mkdir /usr/local/nginx/conf.d

EXPOSE 8088 443

ENV PATH "$PATH:/usr/local/nginx"
CMD ["nginx", "-g", "daemon off;"]
