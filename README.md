# Ibexa DXP on Docker

This helper repository sets up a new Ibexa DXP project for you with a pre-made Docker configuration to get you started quicker.
The official Ibexa meta package installation is executed during install. Ibexa will be placed in the `app` folder. This repository acts as a wrapper that includes a docker development configuration around it.

## Requirements

- Docker installed and running
- Composer installed

## Getting started

During installation, you will be prompted to enter your Ibexa credentials. You can get them in Ibexa's [support panel](https://support.ibexa.co).
The official documentation has [more details on credentials](https://doc.ibexa.co/en/latest/getting_started/requirements/#ibexa-dxp-credentials).

- Recommended option: Store your Ibexa credentials globally `composer config --global http-basic.updates.ibexa.co <installation-key> <token-password>`
- Alternatively, edit the auth.dist.json and save it as auth.json

## Installation

**Step 1**: Pick one flavour of Ibexa. Exceute one of the following commands:

```
composer create-project vardumper/ibexa-on-docker <my-folder> # Installs Ibexa DXP Open Source (default)
composer create-project vardumper/ibexa-on-docker:dev-experience <my-folder> # Installs Ibexa DXP Experience
composer create-project vardumper/ibexa-on-docker:dev-commerce <my-folder> # Installs Ibexa DXP Commerce
composer create-project vardumper/ibexa-on-docker:dev-content <my-folder> # Installs Ibexa DXP Content
```

**Step 2**: Finalizing the installation

```bash
cd <my-folder> # change into the project folder
docker-compose up -d # this will start the containers
docker exec ibexa-php /bin/bash -c "cd /app;php bin/console secrets:generate-keys" # generates app secrets
docker exec ibexa-php /bin/bash -c "cd /app;composer req predis/predis" # installs predis
docker exec ibexa-php /bin/bash -c "cd /app;php bin/console ibexa:install" # finalizes the setup
```

## Accessing the site

http://localhost:8080

## Whats included

As a personal preference I am using the bitnami images for Nginx, PHP and MariaDB.

- Nginx v1.24.0
- PHP-FPM v8.2.7
- MariaDB v10.8.8
- Elasticsearch v8.8.2
- Redis v6.2

## Making adjustments

If you want to run the containers on different ports, you can do so by adjusting the docker-compose.yml file.
If you want to use different container images, feel free to make your adjustments in the docker-compose.yml file, as well.
