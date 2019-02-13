---
title: Set up a Hexo blog on GitHub in 5 minutes
---


## Introuction
[Hexo](https://hexo.io/) is a light-weight blog system designed with Javascript on Node.js. Other than wordpress utilize PHP template and generate context upon the request, so usually need to set cache and other web optimization method. Hexo generate and deploy the context as HTML to server, so it has advantage of speed comparing to Wordpress.

Blew is Pros and Cons
Pros
1. Support mark down syntax, which is handy for writing programming related articles
2. Light Weight
3. Easy deploy on Github and Heroko which are free server
4. Fast to visit

CONS
1. Need more programming skills
2. Need Node.js and Git knowledge

So I consider it as a good blog platform for Geek.

## Create and deploy default website

### Prerequisite
1. GitHub, Heroko or other similar server's accounting
2. [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/) installed on local

### Install Hexo

``` bash
$ npm install -g hexo-cli
```

### Set up on local

Once installed , run following commands to initialise Hexo in the target <folder>.
``` bash
$ hexo init <folder>
$ cd <folder>
$ npm install
```

### Deployment

Suppose using github to server the blogs

#### Modify \_config.yml file
``` bash
deploy:
  type: git
  repo: <repository url>
  branch: [branch]
  message: [message]
```


#### Install [hexo-deployer-git.](https://github.com/hexojs/hexo-deployer-git)
```bash
$ npm install hexo-deployer-git --save
```

Remember --save is mandatory, otherwise git can not work

#### Select a Theme(Optional)

You could select a proper Theme. I use [next](https://github.com/LeonAppDev/hexo-theme-next.git)

#### Deploy to Git

If you use the default theme, then tap below command
``` bash
$ hexo deploy
```

Otherwise read document of your theme carefully and modify your configuration accordingly.

## Quick Start

### Create a new post

``` bash
$ hexo new "My New Post"
```

More info: [Writing](https://hexo.io/docs/writing.html)

### Run server

``` bash
$ hexo server
```

More info: [Server](https://hexo.io/docs/server.html)

### Generate static files

``` bash
$ hexo generate
```

More info: [Generating](https://hexo.io/docs/generating.html)

### Deploy to remote sites

``` bash
$ hexo deploy
```

More info: [Deployment](https://hexo.io/docs/deployment.html)



*Update on 12/Feb/2019
### CNAME
To avoid CNAME is always overriden by new generate and deploy, put a valid CNAME file into source folder.