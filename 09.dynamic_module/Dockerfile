FROM nginx:1.13.12

COPY modules /etc/nginx/modules
RUN chmod 644 /etc/nginx/modules/ngx_http_hello_world_module.so

COPY conf /etc/nginx/conf
RUN rm -rf /etc/nginx/nginx.conf
COPY nginx.conf /etc/nginx/nginx.conf