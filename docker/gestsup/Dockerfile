# GestSup Docker Image
# Based on official documentation: https://doc.gestsup.fr/install/

FROM php:8.2-apache

# Install system dependencies and PHP extensions
RUN apt-get update && apt-get install -y \
    curl \
    unzip \
    wget \
    ntp \
    cron \
    mariadb-client \
    && rm -rf /var/lib/apt/lists/*

# Install PHP extensions required by GestSup
RUN docker-php-ext-install \
    mysqli \
    pdo \
    pdo_mysql \
    && apt-get update && apt-get install -y \
    libcurl4-openssl-dev \
    libgd-dev \
    libc-client-dev \
    libkrb5-dev \
    libintl-dev \
    libldap2-dev \
    libmbstring-dev \
    libxml2-dev \
    libzip-dev \
    && docker-php-ext-configure imap --with-kerberos --with-imap-ssl \
    && docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ \
    && docker-php-ext-install \
    curl \
    gd \
    imap \
    intl \
    ldap \
    mbstring \
    xml \
    zip \
    && rm -rf /var/lib/apt/lists/*

# Configure PHP settings for GestSup
RUN echo "max_execution_time = 480" >> /usr/local/etc/php/conf.d/gestsup.ini \
    && echo "memory_limit = 512M" >> /usr/local/etc/php/conf.d/gestsup.ini \
    && echo "upload_max_filesize = 8M" >> /usr/local/etc/php/conf.d/gestsup.ini \
    && echo "date.timezone = Europe/Paris" >> /usr/local/etc/php/conf.d/gestsup.ini

# Enable Apache modules
RUN a2enmod rewrite ssl

# Create gestsup user and set permissions
RUN groupadd gestsup \
    && useradd -g gestsup gestsup \
    && usermod -a -G www-data gestsup

# Download and extract GestSup
WORKDIR /var/www/html
RUN wget https://gestsup.fr/downloads/versions/current/version/gestsup_3.2.X.zip \
    && unzip gestsup_3.2.X.zip \
    && rm gestsup_3.2.X.zip \
    && rm index.html

# Set proper permissions
RUN chown -R gestsup:www-data /var/www/html/ \
    && find /var/www/html/ -type d -exec chmod 750 {} \; \
    && find /var/www/html/ -type f -exec chmod 640 {} \; \
    && chmod 770 -R /var/www/html/upload \
    && chmod 770 -R /var/www/html/images/model \
    && chmod 770 -R /var/www/html/backup \
    && chmod 770 -R /var/www/html/_SQL \
    && chmod 660 /var/www/html/connect.php

# Create directories for volumes
RUN mkdir -p /var/www/html/upload /var/www/html/backup

# Copy custom Apache configuration if needed
# COPY apache-gestsup.conf /etc/apache2/sites-available/000-default.conf

# Expose port 80
EXPOSE 80 443

# Start Apache
CMD ["apache2-foreground"]