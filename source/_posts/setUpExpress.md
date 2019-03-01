---
title: Set up a Express server using Docker
date: 2019-02-28 15:57:45
tags:
---

## Setup nginx and reverse proxy

I put my customer configuration in :q!nginx configuraion file in /etc/nginx/common_http.conf

## Solve an issue in Docker

Sometimes your docker is running but you have not got the right result, then you need to go inside docker, and need to install vi or netstat in linux using apt-update and then apt-get

And to allow docker to access local resource, we need to run 

```
docker run --net=host -t -d node-web-app
``` 
