---
layout: page
title: Installation
permalink: /installation/
---

There are some different ways you can use to install File Manager on your computer or server. You can choose on the following. After having it installed, take a look at the [configuration](../configuration).

## One-step Script

If you're running a Linux distribution, macOS or any other platform where `curl` or `wget` commands are available, you can use our special script - made by [Kyle Frost](https://www.kylefrost.me/) - to download the latest version of File Manager and install it on `/user/local/bin`.

With curl:

```shell
curl -fsSL https://henriquedias.com/filemanager/get.sh | bash
```

Or using wget:

```
wget -qO- https://henriquedias.com/filemanager/get.sh | bash
```

If you're on Windows, you can use PowerShell to install File Manager too. You should run the following command as administrator since it needs permissions to add the executable to the PATH:

```
iwr -useb https://henriquedias.com/filemanager/get.ps1 | iex
```

## Caddy

The easiest way to get started is using this with Caddy web server. You just need to download Caddy from its [official website](https://caddyserver.com/download) with `http.filemanager` plugin enabled. For more information about the plugin itself, please refer to its [documentation](https://caddyserver.com/docs/http.filemanager).

If you're building Caddy from source, you should import `github.com/hacdias/filemanager/caddy/filemanager` for File Manager, `github.com/hacdias/filemanager/caddy/hugo` for Hugo and `github.com/hacdias/filemanager/caddy/jekyll` for Jekyll.

## Docker

File Manager is also available on Docker through [Docker Hub](https://hub.docker.com/r/hacdias/filemanager/). To install it, run:

```
docker pull hacdias/filemanager
```

The paths you need to bind to do your own configuration are:

- Config: `/etc/config.json`
- Database: `/etc/database.db`
- Base scope: `/srv`

By default, the image uses the configuration file (which is also our recommendation). The **defaults** are:

```json
{
  "port": 80,
  "address": "",
  "database": "/etc/database.db",
  "scope": "/srv",
  "allowCommands": true,
  "allowEdit": true,
  "allowNew": true,
  "commands": []
}
```

Using the configuration file:

```shell
docker run \
    -v /path/to/sites/root:/srv \
    -v /path/to/config.json:/config.json \
    -v /path/to/database.db:/database.db \
    -p 80:80 \
    hacdias/filemanager
```

Using command line arguments:

```shell
docker run \
    -v /path/to/sites/root:/srv \
    -v /path/to/database.db:/database.db \
    -p 80:80 \
    hacdias/filemanager
    --port 80
    --database /database.db
    --scope /srv
    --other-flag other-value
```

