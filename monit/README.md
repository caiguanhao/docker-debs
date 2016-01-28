monit
=====

If you want to use monit web interface,
remember to ban the non-GET requests:

```nginx
server {
	listen 80;
	server_name server;
	location / {
		if ($request_method != "GET") {
			return 403;
		}
		proxy_pass http://127.0.0.1:2812;
	}
}
```
