# Dockerized Ibexa DXP

This is a highly opinionated approach to setting up Ibexa DXP inside Dokcer.

## Requirements

- Docker installed and running
- Composer installed

## Getting started

```bash
composer install # this will install Ibexa DXP into site/ directory
docker-compose up -d # this will start the containers
```

## Whats included

We're using

- PHP 8.2
- MariaDB 10.8
- Nginx

## Accessing the site

localhost:8880

## Making adjustments

If you want to run the containers on different ports, you can do so by adjusting the docker-compose.yml file.
If you want to use different container images, feel free to make your adjustments in the docker-compose.yml file, as well.
