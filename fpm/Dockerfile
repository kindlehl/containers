FROM debian:buster

# Set build args. These will be available as ENV vars in scripts and RUN commands
ARG PHP_VERSION=7.4
# Need to set this as an ENV var to be used by the CMD directive at runtime
ENV PHP_VERSION=$PHP_VERSION

COPY ./scripts /usr/local/bin/

# Run Installation scripts
RUN php-install 

# Configure Opcache
RUN { \ 
    echo 'zend_extension=opcache.so'; \
    echo 'opcache.memory_consumption=128'; \
    echo 'opcache.interned_strings_buffer=16'; \
    echo 'opcache.max_accelerated_files=4000'; \
    echo 'opcache.revalidate_freq=60'; \
    echo 'opcache.fast_shutdown=1'; \
    echo 'opcache.enable_cli=1'; \
  } > /etc/php/$PHP_VERSION/fpm/conf.d/10-opcache.ini

EXPOSE 9000/TCP

CMD /usr/sbin/php-fpm${PHP_VERSION} --daemonize \
    --fpm-config /etc/php/$PHP_VERSION/fpm/php-fpm.conf \
    && tail -f /var/log/php${PHP_VERSION}-fpm.log
