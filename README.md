![CI Workflow](https://github.com/tonyp7/docker-wordpress-fpm-sqlite-nginx/actions/workflows/compose.yml/badge.svg)

# Wordpress Site with SQLite, Nginx and PHP-FPM on Docker

This repository features a docker-compose.yml that allows running very easily a Wordpress website running on php-fpm, Nginx and SQLite.

It makes it easy to run a containerized self-hosted blog.

# How to use

Just simply clone and run!

```bash
git clone https://github.com/tonyp7/docker-wordpress-fpm-sqlite-nginx.git
cd docker-wordpress-fpm-sqlite-nginx
docker compose up --detach
```

By default, the site will run on the 8080 port so you can go to http://localhost:8080 on the local host.

# Docker Images

The repository contains two docker images: wp and nginx.

## Wordpress image

The Wordpress image is based on **wordpress:fpm-alpine**, which itself is based off the **php:fpm-alpine** (at the time of writing, php:8.2-fpm-alpine, although this may change to include newer revisions); which is itself based off **alpine**.
The image will pull the latest version of the official SQlite plugin for Wordpress and install it.
The docker-compose will in addition setup the wp-config.php file so that it can run properly with SQLite.

## Nginx image

The Nginx image is based off the **nginx:stable-alpine** official image. 
It contains a sensible configuration file that hardens and make nginx wordpress friendly. Notably the configuration files:
 - Caches static files
 - Imposes a rate limit on wp-login.php
 - Disable external access to xmlrpc.php
 - Disable running php files inside Wordpress content folders
The configuration provides a solid foundation to any Wordpress website.

# Docker volumes

Two volumes will be created on the first launch: db and html. The first volume contains the SQLite database files, while the html subfolder contains the Wordpress installation. This should make it easy to backup using your favourite method. 
