FROM nginx:1.13.12

ENV VER_NGINX_DEVEL_KIT=0.2.19
ENV VER_NGINX=1.13.12
ENV VER_NAXSI=master

ENV NGINX_DEVEL_KIT ngx_devel_kit-${VER_NGINX_DEVEL_KIT}
ENV NAXSI naxsi-${VER_NAXSI}

RUN apt-get -qq update
RUN apt-get -qq -y install wget

RUN apt-get -qq -y install make
RUN apt-get -qq -y install libpcre3
RUN apt-get -qq -y install libpcre3-dev
RUN apt-get -qq -y install zlib1g-dev
RUN apt-get -qq -y install libssl-dev
RUN apt-get -qq -y install gcc

RUN wget http://nginx.org/download/nginx-${VER_NGINX}.tar.gz
RUN wget https://github.com/simpl/ngx_devel_kit/archive/v${VER_NGINX_DEVEL_KIT}.tar.gz -O ${NGINX_DEVEL_KIT}.tar.gz
RUN wget https://github.com/nbs-system/naxsi/archive/${VER_NAXSI}.tar.gz -O ${NAXSI}.tar.gz

RUN tar -xzvf nginx-${VER_NGINX}.tar.gz && rm nginx-${VER_NGINX}.tar.gz
RUN tar -xzvf ${NGINX_DEVEL_KIT}.tar.gz && rm ${NGINX_DEVEL_KIT}.tar.gz
RUN tar -xzvf ${NAXSI}.tar.gz && rm ${NAXSI}.tar.gz

WORKDIR /nginx-${VER_NGINX}
RUN ./configure --prefix=/etc/nginx --sbin-path=/usr/sbin/nginx --conf-path=/etc/nginx/nginx.conf --add-module=/${NAXSI}/naxsi_src --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log --pid-path=/var/run/nginx.pid --lock-path=/var/run/nginx.lock --http-client-body-temp-path=/var/cache/nginx/client_temp --http-proxy-temp-path=/var/cache/nginx/proxy_temp --http-fastcgi-temp-path=/var/cache/nginx/fastcgi_temp --http-uwsgi-temp-path=/var/cache/nginx/uwsgi_temp --http-scgi-temp-path=/var/cache/nginx/scgi_temp --user=nginx --group=nginx --with-http_ssl_module --with-http_realip_module --with-http_addition_module --with-http_sub_module
RUN make -j2
RUN make install

WORKDIR /${NAXSI}
RUN cp naxsi_config/naxsi_core.rules /etc/nginx

RUN rm -rf /nginx-${VER_NGINX}
RUN rm -rf /${NGINX_DEVEL_KIT}
RUN rm -rf /${NAXSI}