ARG PHP_VERSION
FROM nanoninja/php-fpm:$PHP_VERSION

# Composer
RUN php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');" \
	&& php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && mv composer.phar /bin/composer \
    && composer config -g repo.packagist composer https://packagist.laravel-china.org

WORKDIR /var/software

RUN mkdir -p /var/software \
	&& php -r "copy('https://nodejs.org/dist/v10.13.0/node-v10.13.0-linux-x64.tar.xz','/var/software/nodejs.tar.xz');" \
	&& tar xf nodejs.tar.xz \
    && ln -s ${PWD}/node-v10.13.0-linux-x64/bin/node /usr/local/bin \
    && ln -s ${PWD}/node-v10.13.0-linux-x64/bin/npm /usr/local/bin \
    && ln -s ${PWD}/node-v10.13.0-linux-x64/bin/npmx /usr/local/bin \
    && rm -rf nodejs.tar.xz \
    && docker-php-ext-install pcntl \
    && docker-php-ext-install bcmath \
    && apt-get update \
    && apt-get install -y \
    git

WORKDIR /var/www/html