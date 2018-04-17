FROM ubuntu:16.04

ENV VER_NGINX_DEVEL_KIT=0.2.19
ENV VER_NGINX=1.13.12
ENV VER_NGINX_HELLOWORLD_MODULE=master

ENV NGINX_DEVEL_KIT ngx_devel_kit-${VER_NGINX_DEVEL_KIT}
ENV NGINX_HELLOWORLD_MODULE nginx-hello-world-module-${VER_NGINX_HELLOWORLD_MODULE}

ENV NGINX_ROOT=/nginx
ENV WEB_DIR ${NGINX_ROOT}/html

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
RUN wget https://github.com/yuttasakcom/nginx-hello-world-module/archive/${VER_NGINX_HELLOWORLD_MODULE}.tar.gz -O ${NGINX_HELLOWORLD_MODULE}.tar.gz

RUN tar -xzvf nginx-${VER_NGINX}.tar.gz && rm nginx-${VER_NGINX}.tar.gz
RUN tar -xzvf ${NGINX_DEVEL_KIT}.tar.gz && rm ${NGINX_DEVEL_KIT}.tar.gz
RUN tar -xzvf ${NGINX_HELLOWORLD_MODULE}.tar.gz && rm ${NGINX_HELLOWORLD_MODULE}.tar.gz

WORKDIR /nginx-${VER_NGINX}
RUN ./configure --prefix=${NGINX_ROOT} --add-module=/${NGINX_DEVEL_KIT} --add-module=/${NGINX_HELLOWORLD_MODULE}
RUN make -j2
RUN make install
RUN ln -s ${NGINX_ROOT}/sbin/nginx /usr/local/sbin/nginx

WORKDIR ${WEB_DIR}
EXPOSE 80
EXPOSE 443

RUN rm -rf /nginx-${VER_NGINX}
RUN rm -rf /${NGINX_DEVEL_KIT}
RUN rm -rf /${NGINX_HELLOWORLD_MODULE}

CMD ["nginx", "-g", "daemon off;"]