# Verdaccio and simple local storage

This example shows a simple configuration for `verdaccio` plus the default local storage with the minimum configuration required using `docker-compose`.

Contains

* conf: Configuration file and default user httpasswd
* storage: A published default package with 2 versions.

```bash
$> docker-compose up
```

## Login

If you want to login into the Verdaccio instance created via these Docker Examples, please try:

Username: jpicado
Password: jpicado

## Running in Dokku

If you use Dokku, an open-source alternative for Heroku, you can run this example using the following steps:

1. Create a new application `dokku apps:create verdaccio`
2. Pull the verdaccio image `docker pull verdaccio/verdaccio:`
3. Tag the docker image for the app: `docker tag verdaccio/verdaccio:4 dokku/verdaccio:v1`
4. Create the directories for persistent storage `mkdir -p /var/lib/dokku/data/storage/verdaccio/storage`, `mkdir -p /var/lib/dokku/data/storage/verdaccio/storage`
5. Mount the volumes: `dokku storage:mount verdaccio /var/lib/dokku/data/storage/verdaccio/storage:/verdaccio/storage` and `dokku storage:mount verdaccio /var/lib/dokku/data/storage/verdaccio/conf:/verdaccio/conf`
4. Deploy the docker image `dokku tags:deploy verdaccio v1`
5. Enjoy the application


## Issue

1. 'Error: EACCES: permission denied, open \'/verdaccio/storage/.verdaccio-db.json\'

solution:
```
chmod 777 -R storage/
```

2. 在config目录下添加一个空的htpasswd文件，并添加权限
```
chmod 777 -R config/htpasswd
```

## 如何发布一个npm包
- [How to make a beautiful, tiny npm package and publish it](https://medium.com/free-code-camp/how-to-make-a-beautiful-tiny-npm-package-and-publish-it-2881d4307f78)

## 入口Docker依赖
 - https://github.com/evertramos/docker-compose-letsencrypt-nginx-proxy-companion
