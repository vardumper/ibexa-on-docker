FROM docker.io/bitnami/php-fpm:8.2.8

ENV PHP_MEMORY_LIMIT="512M"

RUN apt-get update && apt-get upgrade -y
RUN apt-get install --no-install-recommends autoconf build-essential wget=1.21 unzip=6.00 nano=5.4 ${PHPIZE_DEPS} make=4.3 libpcre2-posix2 libpcre2-dev -yq
# cmake=3.18.4 gcc=10.2.1 g++=10.2.1
RUN cd /root \
    && wget -nv https://pecl.php.net/get/redis-5.3.7.tgz \
    && tar xzf redis-5.3.7.tgz && cd redis-5.3.7 \
    && phpize \
    && ./configure \
    && make \
    && make install
RUN echo "extension=redis.so" >> /opt/bitnami/php/etc/php.ini

# Install Composer
COPY --from=library/composer /usr/bin/composer /usr/local/bin/composer

# Install NodeJS and Yarn
COPY --from=library/node:18.4 /usr/local/bin/node /usr/local/bin/node
COPY --from=library/node:18.4 /usr/local/include/node /usr/local/include/node
COPY --from=library/node:18.4 /usr/local/lib/node_modules /usr/local/lib/node_modules
COPY --from=library/node:18.4 /opt/yarn-v*/bin/* /usr/local/bin/
COPY --from=library/node:18.4 /opt/yarn-v*/lib/* /usr/local/lib/

# Copy entrypoint
COPY --from=library/node:18.4 /usr/local/bin/docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh

RUN ln --symbolic ../lib/node_modules/npm/bin/npm-cli.js /usr/local/bin/npm \
    && ln --symbolic ../lib/node_modules/npm/bin/npx-cli.js /usr/local/bin/npx
