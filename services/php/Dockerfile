FROM php:7.4-fpm

# 设置时区
ENV TZ=Asia/Shanghai
# 安装 Composer
ENV COMPOSER_HOME /root/composer
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone \
        && apt-get update && apt-get install -y \
        --no-install-recommends libfreetype6-dev libjpeg62-turbo-dev libpng-dev curl \
        && rm -r /var/lib/apt/lists/* \
        && docker-php-ext-configure gd \
        && docker-php-ext-install -j$(nproc) gd opcache pdo_mysql gettext sockets \
        && pecl install redis \
        && pecl install swoole \
        && docker-php-ext-enable redis swoole \
        && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
ENV PATH $COMPOSER_HOME/vendor/bin:$PATH

WORKDIR /www
RUN git clone git@gitee.com:ZhongBangKeJi/CRMEB.git \
    && composer install