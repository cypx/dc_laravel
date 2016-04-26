FROM php:5.6-apache

RUN requirements="libldap-2.4-2 libldap2-dev libmcrypt-dev" \
   && apt-get update && apt-get install -y $requirements && rm -rf /var/lib/apt/lists/* \
   && ln -fs /usr/lib/x86_64-linux-gnu/libldap.so /usr/lib/ \
   && docker-php-ext-install -j$(nproc) mcrypt \
   && docker-php-ext-install ldap

RUN a2enmod rewrite
