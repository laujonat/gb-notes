---
description: Basic commands for network requests
---

# Network Requests

## Getting Started

On Ubuntu and Debian derived systems, you can install it using the following commands:

```text
sudo apt update
sudo apt install libwww-perl
```

On CentOS, Rocky Linux, Fedora, and other RedHat derived systems, you can install it with support for HTTPS URLs using the following command:

```text
sudo dnf install perl-libwww-perl.noarch perl-LWP-Protocol-https.noarch
```

### `GET` <a id="get"></a>

Let’s say you loved the Alligator.io logo so much, you wanted to download it locally. It’s a pretty amazing logo, who wouldn’t want their own personal copy?

To `GET` the file, you can simply run:

```text
GET https://alligator.io/images/logo-fancy.svg
```

Not so fast! All that does is show a bunch of SVG markup.

In true Unix Philosophy fashion, the `GET` command does one thing really well and that’s `GET`ting a file.

This is great when you want to check a URL to see what’s being returned by the web server, but if you want to truly download that lovely logo, you’ll want to send the output to a file:

```text
GET https://alligator.io/images/logo-fancy.svg > logo-fancy.svg
```

Now we have that fantastic Alligator.io logo downloaded to a local file!

### `POST` <a id="post"></a>

The `GET` command allows us to consume files from remote servers while `POST` allows us to send data to a server for processing as well as return it’s output.

At it’s very least, the syntax for `POST` is the same as `GET`:

```text
POST https://httpbin.org/post
```

 

This will then prompt you for the content you’d like to `POST`. The string expected should be in a query string format that looks something like this:

```text
reptile=alligator&color=#008f68
```

When you’re done entering in your content, simply hit `CTRL-D` and the content will be `POST`ed. The service we’re posting to will mirror back the request:

```text
{
  "args": {},
  "data": "",
  "files": {},
  "form": {
    "color": "#008f68\n",
    "reptile": "alligator"
  },
  "headers": {
    "Content-Length": "32",
    "Content-Type": "application/x-www-form-urlencoded",
    "Host": "httpbin.org",
    "User-Agent": "lwp-request/6.39 libwww-perl/6.39"
  },
  "json": null,
  "origin": "203.0.113.5",
  "url": "https://httpbin.org/post"
}
```

 Copy

### `HEAD` <a id="head"></a>

As mentioned, `HEAD` is not only extremely useful for debugging and troubleshooting, but I’m pretty sure it’s in my top 5 all-time favorite command-line utilities.

Similar to `GET` and `POST`, the syntax for `HEAD` is quite minimal:

```text
HEAD http://alligator.io/
```

 

This will return a `200 OK` and information about the headers returned by the web service.

Unfortunately, this isn’t quite right, because we serve up Alligator.io over HTTPS like the good security-minded reptilian webizens that we are.

The `HEAD` command by default only gives you information about the last stop in the request chain. To see all of the requests, including the automatic `301 Moved Permanently`, pass in the `-S` argument:

```text
HEAD -S http://alligator.io/
```

 

Which gives us a bit more insight:

```text
OutputHEAD http://alligator.io/
301 Moved Permanently
HEAD https://alligator.io/
200 OK
Cache-Control: public, max-age=0, must-revalidate
Connection: close
Date: Sat, 29 Jun 2019 00:49:18 GMT
Age: 1
ETag: "8b85849c835909679fc1ba80b307d144-ssl"
Server: Netlify
Content-Length: 0
Content-Type: text/html; charset=UTF-8
Client-Date: Sat, 29 Jun 2019 00:49:18 GMT
Client-Peer: 203.0.113.1:443
Client-Response-Num: 1
Client-SSL-Cert-Issuer: /C=US/O=Let's Encrypt/CN=Let's Encrypt Authority X3
Client-SSL-Cert-Subject: /CN=alligator.io
Client-SSL-Cipher: TLS_AES_256_GCM_SHA384
Client-SSL-Socket-Class: IO::Socket::SSL
Strict-Transport-Security: max-age=31536000
X-NF-Request-ID: 60babe56-c0ea-4658-aa5a-3e185f1e851f-10342
```

### Bonus <a id="bonus"></a>

Monochromatic output got you down? If so, you could alias [HTTPie](https://httpie.org/)’s `http` command to `GET`, `POST` and `HEAD`.

HTTPie can do everything the `lwp-request` library does, with similar syntax, with the added bonus of colorful output.

On Ubuntu and Debian derived systems you can install HTTPie with the following commands:

```text
sudo apt update
sudo apt install httpie
```

On Centos, Rocky Linux, Fedora, and RedHat derived distributions you can install HTTPie using the following commands, as long as you have the EPEL :

```text
sudo dnf install epel-release
sudo dnf install httpie
```

 

My local aliases look like this:

```text
# HTTPie aliases
alias GET='http'
alias POST='http POST'
alias HEAD='http HEAD'
```

### Conclusion <a id="conclusion"></a>

Next time you need to make a network request to an API or are troubleshooting the headers returned by a server, you can leave Postman and similar tools at the door.

You can omit your browser entirely, too!

