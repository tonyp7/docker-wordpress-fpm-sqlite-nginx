FROM wordpress:fpm-alpine

# Set Process Manager to "ondemand"
# RUN sed -i 's/pm = dynamic/pm = ondemand/g' /usr/local/etc/php-fpm.d/www.conf

# Install curl and unzip
RUN apk add --update curl unzip && rm -Rf /var/cache/apk/*

# Download the Sqlite integration plugin
RUN curl -o /tmp/wpplugin.zip https://downloads.wordpress.org/plugin/sqlite-database-integration.zip
RUN unzip /tmp/wpplugin.zip -d /usr/src/wordpress/wp-content/plugins/
RUN rm /tmp/wpplugin.zip

# Setup
RUN cp /usr/src/wordpress/wp-content/plugins/sqlite-database-integration/db.copy /usr/src/wordpress/wp-content/db.php

# make sure we set these to the right owner
RUN chown -R www-data:www-data /var/www/html
RUN mkdir /var/www/db
RUN chown -R www-data:www-data /var/www/db
VOLUME ["/var/www/db"]