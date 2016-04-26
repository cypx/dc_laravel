FROM composer/composer

RUN apt-get update && \
  DEBIAN_FRONTEND=noninteractive apt-get install -y libldap-2.4-2 libldap2-dev

RUN ln -fs /usr/lib/x86_64-linux-gnu/libldap.so /usr/lib/

RUN docker-php-ext-install ldap
