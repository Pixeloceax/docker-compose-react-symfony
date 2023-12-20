# Utilisez une image de base avec PHP et Apache
FROM php:8.2-apache

# Installez les dépendances nécessaires pour Symfony
RUN apt-get update && apt-get install -y \
    libicu-dev \
    libpq-dev \
    libzip-dev \
    zlib1g-dev \
    unzip \
    wget \
    curl

# Installez les extensions PHP nécessaires pour Symfony
RUN docker-php-ext-install intl
RUN docker-php-ext-install pdo_pgsql
RUN docker-php-ext-install zip


# Activez le module Apache mod_rewrite
RUN a2enmod rewrite

# Copiez les fichiers de l'application dans le conteneur
COPY . /var/www/html

# Définissez le répertoire de travail
WORKDIR /var/www/html

# Installez les dépendances du projet Symfony
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer install --no-scripts --no-autoloader

# Installez Symfony CLI
RUN wget https://get.symfony.com/cli/installer -O - | bash
RUN export PATH="$HOME/.symfony5/bin:$PATH"

# Générez les fichiers d'autoloading et les assets
RUN composer dump-autoload --optimize
RUN php bin/console assets:install --symlink

# Exposez le port 80 pour accéder à l'application
EXPOSE 80

CMD ["sh", "-c", "apache2-foreground"]
