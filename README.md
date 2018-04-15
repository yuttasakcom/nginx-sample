# Nginx Sample

## Table of Content

* [Useful Command](#useful-command)
* [Directives](#directives)
* [Nginx Site](#nginx-site)
* [Location](https://github.com/yuttasakcom/nginx-sample/tree/master/02.location)
* Reverse Proxy
* Load Balance
* Caching
* Ratelimit
* SSL

## Useful Command

```bash
$ nginx -s stop # หยุดการทำงาน nginx
$ nginx -s reload # ใช้เมื่อมีการแก้ไข config ของ nginx
$ nginx -t # ตรวจสอบค่า config nginx ก่อนสั่ง reload
$ service nginx start|stop|restart # สั่งงาน nginx ผ่าน service
```

## Directives

```
ยกตัวอย่างแค่ http, server, upstream
===== http ================================
Syntax:	http { ... } # ตัวอย่างการประกาศใช้งาน
Default:	— # ไม่มีการกำหนดค่า default
Context:	main # เป็น main directive ไม่อยู่ภายใต้ใคร

===== server ==============================
Syntax:	server { ... } # ตัวอย่างการประกาศใช้งาน
Default:	— # ไม่มีการกำหนดค่า default
Context:	http # อยู่ภายใต้ http เช่น http { server { ... } }

===== upstream ============================
Syntax:	upstream name { ... } # ตัวอย่างการประกาศใช้งาน
Default:	— # ไม่มีการกำหนดค่า default
Context:	http # อยู่ภายใต้ http เช่น http { upstream name { ... } }
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
