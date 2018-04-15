# Nginx Site

## Start Docker

```bash
$ docker-compose up -d
```

## Test

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

## Summary

* ควรแยก config site แต่ละ site เป็น 1 config file เก็บไว้ใน conf/site/
* แก้ไข nginx.conf จาก include /etc/nginx/conf.d/\*.conf; เป็น include conf/site/\*;
