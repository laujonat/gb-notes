---
description: >-
  In this guide, we’ll discuss how to install Nginx on your Ubuntu 20.04 server,
  adjust the firewall, manage the Nginx process, and set up server blocks for
  hosting more than one domain from a single se
---

# Nginx

## Introduction

[Nginx](https://www.nginx.com/) is one of the most popular web servers in the world and is responsible for hosting some of the largest and highest-traffic sites on the internet. It is a lightweight choice that can be used as either a web server or reverse proxy.



Edit 

```text
$ vim /etc/nginx/sites-available/default
```

Verify changes

```text
$ nginx -t
```

### Deploy using Docker Host

```text
 $ docker build -t fastapi
 $ docker run -d -p 8000:80 --name fastapi nginx
```



