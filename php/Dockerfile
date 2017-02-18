FROM php:7.1-apache

MAINTAINER Utkarsh Vishnoi <utkarshvishnoi25@gmail.com>

# System update and upgrade
RUN apt update
RUN apt upgrade -y

# Install ssmtp and integrate with php
RUN apt install ssmtp -y && \
    echo "sendmail_path = /usr/sbin/ssmtp -t" > /usr/local/etc/php/conf.d/sendmail.ini && \
    echo "mailhub=lemptest_mailcatcher_1:25\nUseTLS=NO\nFromLineOverride=YES" > /etc/ssmtp/ssmtp.conf

# Installed Mysql Extension
RUN docker-php-ext-install pdo_mysql


# Installing mcrypt, iconv and gd
RUN apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
    && docker-php-ext-install -j$(nproc) iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd