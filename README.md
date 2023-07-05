# Dockerized Ibexa DXP

This is a highly opinionated approach to setting up Ibexa DXP inside Dokcer.
Ibexa will be installed into a `ibexa/` directory.

## Requirements

- Docker installed and running
- Composer installed

## Getting started

During installation, you will be prompted to enter your Ibexa credentials. You can find these in the support.ibexa.co portal.
See the official documentation, on how to get your credentials: https://doc.ibexa.co/en/latest/getting_started/requirements/#ibexa-dxp-credentials

**TLDR:**

- Recommended option: Store your Ibexa credentials globally `composer config --global http-basic.updates.ibexa.co <installation-key> <token-password>`
- Alternative option: Edit auth.dist.json file and save it as auth.json

## Installation

```bash
composer create-project vardumper/ibexa-on-docker:"<flavour>"
docker-compose up -d # this will start the containers
docker exec ibexa-php /bin/bash -c "cd /var/www/html;php bin/console ibexa:install" # finalizes the setup
```

## Accessing the site

http://localhost:8080

## Whats included

As a personal preference I am using the bitnami images for Nginx, PHP and MariaDB.

- PHP-FPM v8.2.7
- MariaDB v10.8.8
- Nginx v1.24.0
- Redis v6.2

## Making adjustments

If you want to run the containers on different ports, you can do so by adjusting the docker-compose.yml file.
If you want to use different container images, feel free to make your adjustments in the docker-compose.yml file, as well.
