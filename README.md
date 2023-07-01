# Dockerized Ibexa DXP

This is a highly opinionated approach to setting up Ibexa DXP inside Dokcer.
Ibexa will be installed into a `site/` directory.

## Requirements

- Docker installed and running
- Composer installed

## Getting started

```bash
composer install # this will install Ibexa DXP into site/ directory
docker-compose up -d # this will start the containers
```

## Whats included

As a personal preference I am using the bitnami images for Nginx, PHP and MariaDB.

- PHP-FPM v8.2
- MariaDB v10.8
- Nginx v1.21

## Accessing the site

http://localhost:8080

## Making adjustments

If you want to run the containers on different ports, you can do so by adjusting the docker-compose.yml file.
If you want to use different container images, feel free to make your adjustments in the docker-compose.yml file, as well.
