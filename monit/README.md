monit
=====

The monit web interface has been simplified.

I have removed the "buttons" in the web interface, but the API is still untouched.
This is because the monit command uses the same API. Removing these API means
you can use monit command like `monit unmonitor -g delayed_jobs`.

So currently a workaround would be to only allow GET requests:

```nginx
server {
	listen 80;
	server_name server;
	location / {
		if ($request_method !~ ^GET$ ) {
			return 404;
		}
		proxy_pass http://127.0.0.1:2812;
	}
}
```
