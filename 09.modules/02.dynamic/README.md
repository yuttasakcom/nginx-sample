# Nginx Dynamic Modules

## Start Docker

```bash
$ docker-compose up -d --build
```

## Reference

> https://www.nginx.com/blog/compiling-dynamic-modules-nginx-plus/

## Issue

```
HTTP/1.1 200 OK
Server: nginx/1.13.12
Date: Mon, 16 Apr 2018 07:37:38 GMT
Content-Type: text/plain
Content-Length: 12
Connection: keep-alive

Warning: Binary output can mess up your terminal. Use "--output -" to tell
Warning: curl to output it to your terminal anyway, or consider "--output
Warning: <FILE>" to save to a file.
```
