ARG PHP_VERSION
FROM nanoninja/php-fpm:$PHP_VERSION

# Composer
RUN php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');" \
	&& php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && mv composer.phar /bin/composer \
    && composer config -g repo.packagist composer https://packagist.laravel-china.org \
    && composer global require deployer/deployer \
    && composer global require phpunit/phpunit

ENV PATH $PATH:~/.composer/vendor/bin

WORKDIR /usr/local

RUN php -r "copy('https://nodejs.org/dist/v10.13.0/node-v10.13.0-linux-x64.tar.xz','/usr/local/nodejs.tar.xz');" \
	&& tar xf nodejs.tar.xz \
    && cp -r node-v10.13.0-linux-x64/* . \
    && rm -rf node-v10.13.0-linux-x64 \
    && rm -rf nodejs.tar.xz \
    && php -r "copy('https://github.com/yarnpkg/yarn/releases/download/v1.15.2/yarn-v1.15.2.tar.gz','/usr/local/yarn.tar.gz');" \
    && tar xf yarn.tar.gz \
    && rm -rf yarn.tar.gz \
    && docker-php-ext-install pcntl \
    && docker-php-ext-install bcmath \
    && apt-get update \
    && apt-get install -y \
    git \
    unzip \
    vim

ENV PATH $PATH:/usr/local/yarn-v1.15.2/bin
WORKDIR /var/www/html