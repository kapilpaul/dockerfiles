# PHPUnit Docker Container.
FROM alpine:3.8
LABEL mantainer="Rahul Prajapati <rahul.prajapati@live.in>"

LABEL name="phpunit-7.5.20"

ENV PEAR_PACKAGES foo

WORKDIR /tmp

RUN	echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories && \
    apk update && \
	apk upgrade && \
	apk add --update --no-cache \
        bash \
        ca-certificates \
        curl \
        git \
        subversion \
        php7.4 \
        php7.4-bcmath \
        php7.4-ctype \
        php7.4-curl \
        php7.4-dom \
        php7.4-exif \
        php7.4-fileinfo \
        php7.4-iconv \
        php7.4-json \
        php7.4-mbstring \
        php7.4-mcrypt \
        php7.4-mysqli \
        php7.4-opcache \
        php7.4-openssl \
        php7.4-pcntl \
        php7.4-pdo \
        php7.4-pdo_mysql \
        php7.4-pdo_pgsql \
        php7.4-pdo_sqlite \
        php7.4-phar \
        php7.4-session \
        php7.4-simplexml \
        php7.4-soap \
        php7.4-tokenizer \
        php7.4-xdebug \
        php7.4-xml \
        php7.4-xmlreader \
        php7.4-xmlwriter \
        php7.4-zip \
        php7.4-zlib \
        unzip \
        mariadb-client \
        php7.4-memcached \
        php7.4-phpdbg \
        sqlite-dev \
        wget \
    && php -r "copy('https://pear.php.net/go-pear.phar', 'go-pear.phar');" \
    && php go-pear.phar \
    && php -r "unlink('go-pear.phar');" \
    && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php --install-dir=/usr/bin --filename=composer \
    && php -r "unlink('composer-setup.php');" \
    && composer require "phpunit/phpunit:7.5.20" --prefer-source --no-interaction \
    && composer require "phpunit/php-invoker" --prefer-source --no-interaction \
		&& composer require --dev yoast/phpunit-polyfills \
    && ln -s /tmp/vendor/bin/phpunit /usr/local/bin/phpunit \
    && sed -i 's/nn and/nn, Rahul Prajapati (Docker) and/g' /tmp/vendor/phpunit/phpunit/src/Runner/Version.php \
    # Enable X-Debug
    && sed -i 's/\;z/z/g' /etc/php7.4/conf.d/xdebug.ini \
    && php -m | grep -i xdebug

ONBUILD RUN \
    { \
        [ "${PEAR_PACKAGES}" != "foo" ]; \
    } || exit 0 && pear install ${PEAR_PACKAGES}

VOLUME ["/app"]

WORKDIR /app

CMD ["/bin/true"]
