---
title: Solve Cross Origin Resource Share issue
date: 2019-03-16 14:32:11
tags:
---

## Setup on server

You need to add 'Access-Control-Allow-Origin' and other setting in response header from server

## Setup on client

The most elegant solution is to add header in request, but I have falied to do it now, so another work around is using below plugin.

```
In addition to what awd mentioned about getting the person responsible for the server to reconfigure (an impractical solution for local development) I use a change-origin chrome plugin like this:

https://chrome.google.com/webstore/detail/moesif-origin-cors-change/digfbfaphojjndkpccljibejjbppifbc

You can make your local dev server (ex: localhost:8080) to appear to be coming from 172.16.1.157:8002 or any other domain.
```

and we need to do the setting as https://imgur.com/a/Rq51wg6