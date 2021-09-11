---
description: >-
  In this guide, we’ll discuss how to install Nginx on your Ubuntu 20.04 server,
  adjust the firewall, manage the Nginx process, and set up server blocks for
  hosting more than one domain from a single se
---

# Nginx

## Introduction

[Nginx](https://www.nginx.com/) is one of the most popular web servers in the world and is responsible for hosting some of the largest and highest-traffic sites on the internet. It is a lightweight choice that can be used as either a web server or reverse proxy.



#### Start Nginx[\#](https://www.keycdn.com/support/nginx-commands#start-nginx) <a id="start-nginx"></a>

Starting Nginx is very simple. Just use the following command:

```text
service nginx start
```

If you're using a systemd based version such as Ubuntu Linux 16.04 LTS and above, use `systemctl` within the command, like so:

```text
systemctl start nginx
```

**Example response:**

```text
Starting nginx server...
```

#### Stop Nginx[\#](https://www.keycdn.com/support/nginx-commands#stop-nginx) <a id="stop-nginx"></a>

Stopping Nginx will kill all system processes quickly. This will terminate Nginx even if there are open connections. In order to do so, run one of the following commands:

```text
service nginx stop
systemctl stop nginx
```

**Example response:**

```text
Stopping nginx Server...
```

This command can still, however, take some time on busy servers. Therefore, if you want Nginx to stop even faster, you can also use:

```text
killall -9 nginx
```

#### Quit Nginx[\#](https://www.keycdn.com/support/nginx-commands#quit-nginx) <a id="quit-nginx"></a>

Quitting Nginx is very similar to stopping it however it does so gracefully which means it will finish serving open connections before shutting down. To quit Nginx, use one of the following commands:

```text
service nginx quit
systemctl quit nginx
```

#### Restart Nginx[\#](https://www.keycdn.com/support/nginx-commands#restart-nginx) <a id="restart-nginx"></a>

Restarting Nginx basically performs a stop then a start. Use one of the following commands to run an Nginx restart:

```text
service nginx restart
systemctl restart nginx
```

**Example response:**

```text
Stopping nginx Server... [ OK ]
Starting nginx Server... [ OK ]
```

#### Reload Nginx[\#](https://www.keycdn.com/support/nginx-commands#reload-nginx) <a id="reload-nginx"></a>

Reload is a bit different from restart in that, again, it is more gracefully. According to Nginx, reload is defined as "start the new worker process with a new configuration, gracefully shut down old worker processes.". You can reload Nginx by using one of the following commands:

```text
service nginx reload
systemctl reload nginx
```

**Example response:**

```text
Reloading nginx Server... [ OK ]
```

#### View server status[\#](https://www.keycdn.com/support/nginx-commands#view-server-status) <a id="view-server-status"></a>

Check what the current status of your Nginx web server is with one of the following commands:

```text
service nginx status
systemctl status nginx
```

**Example response:**

```text
nginx is running
```

Edit 

```text
$ vim /etc/nginx/sites-available/default
```

Verify changes

```text
$ nginx -t
```

### 

### 

### Deploy using Docker Host

```text
 $ docker build -t fastapi
 $ docker run -d -p 8000:80 --name fastapi nginx
```



