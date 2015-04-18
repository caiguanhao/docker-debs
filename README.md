docker-debs
===========

This is under experiment.

Get deb files in a Docker container.

Change the base system if you are not using Ubuntu 14.04.

Some Dockerfiles are using sources for Chinese users to download packages.
You can change them if there are slow in your location.

Run these commands and the deb files will be put in `/srv/downloads`:

```
docker-compose build
docker-compose up
```

LICENSE: MIT
