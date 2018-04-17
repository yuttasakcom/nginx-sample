FROM nginx:1.13.12

RUN apt update && apt install -y gcc make libpcre3 libpcre3-dev zlib1g-dev

COPY modules/ /etc/nginx/modules
COPY nginx.conf /etc/nginx/nginx.conf
COPY conf.d/ /etc/nginx/conf.d
COPY naxsi/naxsi_core.rules /etc/nginx/naxsi/naxsi_core.rules