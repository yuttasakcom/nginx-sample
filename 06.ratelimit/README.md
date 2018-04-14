# Nginx Ratelimit

## Limit Bandwidth

```bash
$ wget http://example.com/yoyea.zip
```

## Limit Connection

```bash
$ wrk -c 200 -d 1m http://example.com/
```

## Limit Request

```bash
$ ab -c 1 -n 500 http://example.com/yoyea.zip
```
