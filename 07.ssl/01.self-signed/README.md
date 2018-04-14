```bash
$ openssl req -newkey rsa:2048 -x509 -nodes -keyout ./ssl/private.key -new -out ./ssl/public.pem -subj /CN=example.com -sha256 -days 365
```
