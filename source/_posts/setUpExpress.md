---
title: Set up a Express server using Docker
date: 2019-02-28 15:57:45
tags:
---

## Setup nginx and reverse proxy

I put my customer configuration in nginx configuraion file in /etc/nginx/common_http.conf.

Nginx configuration is quite important for reverse proxy, you need to read through the configuraion, since lacation has complicated match rules. I met an issue when I set a location part ```location /nodeapp/ {
}```, but /nodeapp/app-docs/swagger-ui-init.js does not go into this location, at first I thought it is because swagger-ui-express uses related route, but then I find out localhost:3000/app-docs/swagger-ui-inti.js is good to go, and I also use ```curl localhost:3000/app-docs/swagger-ui-inti.js``` in linux server and it gets the javascript file as well, so finally I find out it is because there is another location rule ``` location ~* \.(?:css|js)$```. This article describes how it works [一文弄懂Nginx的location匹配](https://segmentfault.com/a/1190000013267839)




## Solve an issue in Docker

Sometimes your docker is running but you have not got the right result, then you need to go inside docker, and need to install vi or netstat in linux using apt-update and then apt-get

And to allow docker to access local resource, we need to run 

```
docker run --net=host -t -d node-web-app
``` 


## Create a shell script to exucte Docker image create and container launch

## Add a logger system using winston

It is quite handy to use winston to add a logger system, you could define logger level and how to export log in different stage when you define a logger and easy to modify the configutation in future.