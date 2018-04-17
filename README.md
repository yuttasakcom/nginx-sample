# Nginx Sample

## Table of Content

* [Install](#install)
* [Useful Command](#useful-command)
* [Directives](#directives)
* [Nginx Site](#nginx-site)
* [Location](https://github.com/yuttasakcom/nginx-sample/tree/master/02.location)
* [Reverse Proxy](https://github.com/yuttasakcom/nginx-sample/tree/master/03.reverse-proxy)
* [Load Balance](https://github.com/yuttasakcom/nginx-sample/tree/master/04.load-balance)
  * [Round Robin](https://github.com/yuttasakcom/nginx-sample/tree/master/04.load-balance/01.round-robin)
  * [Health Checks](https://github.com/yuttasakcom/nginx-sample/tree/master/04.load-balance/02.healt-checks)
* [Caching](https://github.com/yuttasakcom/nginx-sample/tree/master/05.caching)
  * [No Cache](https://github.com/yuttasakcom/nginx-sample/tree/master/05.caching/01.no-cache)
  * [Cache Set Expries](https://github.com/yuttasakcom/nginx-sample/tree/master/05.caching/02.cache-time)
  * [Proxy Cache](https://github.com/yuttasakcom/nginx-sample/tree/master/05.caching/03.cache)
* [Ratelimit](https://github.com/yuttasakcom/nginx-sample/tree/master/06.ratelimit)
  * [Limit Bandwidth](https://github.com/yuttasakcom/nginx-sample/tree/master/06.ratelimit/01.bandwidth)
  * [Limit Connection](https://github.com/yuttasakcom/nginx-sample/tree/master/06.ratelimit/02.connection)
  * [Limit Request](https://github.com/yuttasakcom/nginx-sample/tree/master/06.ratelimit/03.request)
* [SSL](https://github.com/yuttasakcom/nginx-sample/tree/master/07.ssl)
  * [Self Signed](https://github.com/yuttasakcom/nginx-sample/tree/master/07.ssl/01.self-signed)
  * [Letsencrypt](https://github.com/yuttasakcom/nginx-sample/tree/master/07.ssl/02.letsencrypt)
  * Certbot
* [Websocket](https://github.com/yuttasakcom/nginx-sample/tree/master/08.websocket)
* [Modules](https://github.com/yuttasakcom/nginx-sample/tree/master/09.modules)
  * [Static](https://github.com/yuttasakcom/nginx-sample/tree/master/09.modules/01.static)
  * [Dynamic](https://github.com/yuttasakcom/nginx-sample/tree/master/09.modules/02.dynamic)
* [WAF](https://github.com/yuttasakcom/nginx-sample/tree/master/10.waf)
* [Lua](https://github.com/yuttasakcom/nginx-sample/tree/master/11.lua)
* [Openresty](https://github.com/yuttasakcom/nginx-sample/tree/master/12.openresty)

## Install

### Ubuntu

```bash
$ sudo apt update && sudo apt dist-upgrade && sudo apt autoremove
$ cd /tmp/ && wget http://nginx.org/keys/nginx_signing.key
$ sudo apt-key add nginx_signing.key
$ sudo sh -c "echo 'deb http://nginx.org/packages/mainline/ubuntu/ '$(lsb_release -cs)' nginx' > /etc/apt/sources.list.d/nginx.list"
$ sudo apt update
$ sudo apt install nginx
```

## Useful Command

```bash
$ nginx -s stop # หยุดการทำงาน nginx
$ nginx -s reload # ใช้เมื่อมีการแก้ไข config ของ nginx
$ nginx -t # ตรวจสอบค่า config nginx ก่อนสั่ง reload
$ service nginx start|stop|restart # สั่งงาน nginx ผ่าน service
```

## Directives

> https://nginx.org/en/docs/

```
ยกตัวอย่างแค่ http, server, upstream
===== http ================================
Syntax:	http { ... } # ตัวอย่างการประกาศใช้งาน
Default: — # ไม่มีการกำหนดค่า default
Context: main # เป็น main directive ไม่อยู่ภายใต้ใคร

===== server ==============================
Syntax:	server { ... } # ตัวอย่างการประกาศใช้งาน
Default: — # ไม่มีการกำหนดค่า default
Context: http # อยู่ภายใต้ http เช่น http { server { ... } }

===== upstream ============================
Syntax:	upstream name { ... } # ตัวอย่างการประกาศใช้งาน
Default: — # ไม่มีการกำหนดค่า default
Context: http # อยู่ภายใต้ http เช่น http { upstream name { ... } }
```

## Nginx Site

> https://github.com/yuttasakcom/nginx-sample/tree/master/01.site

### Start Docker

```bash
$ docker-compose up -d
```

### Test

```bash
$ curl localhost -H 'Host: example.com'

===== output =====
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Nginx Site</title>
</head>
<body>
  <p>example.com</p>
</body>
```

### Summary

* ควรแยก config site แต่ละ site เป็น 1 config file เก็บไว้ใน conf/site/
* แก้ไข nginx.conf จาก include /etc/nginx/conf.d/\*.conf; เป็น include conf/site/\*;
