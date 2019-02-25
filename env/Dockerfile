FROM medicean/vulapps:base_lamp_php7
MAINTAINER Medici.Yan <Medici.Yan@Gmail.com> & avfisher

ARG WP_URL=https://wordpress.org/wordpress-4.9.8.tar.gz
ARG WPCLI_URL=http://vulapps.xuanbo.cc/w/wordpress/wp-cli/wp-cli.phar


COPY src/wordpress.sql /tmp/wordpress.sql
COPY src/apache2.conf /etc/apache2/apache2.conf
RUN set -x \
    && apt update \
    && apt-get install -y php-imagick php7.0-fpm unzip wget \
    && ln -s /etc/apache2/mods-available/rewrite.load /etc/apache2/mods-enabled/ \
    && rm -rf /var/www/html/* \
    && wget -qO /tmp/wordpress.tar.gz  $WP_URL \
    && tar -zxf /tmp/wordpress.tar.gz -C /var/www/html --strip-components=1 \
    && rm -rf /tmp/wordpress.tar.gz \
    && service php7.0-fpm reload \
    && service apache2 restart

COPY src/.htaccess /var/www/html/.htaccess
COPY src/wp-config.php /var/www/html/wp-config.php


RUN set -x \
    && wget -qO /usr/bin/wp $WPCLI_URL \
    && chmod a+x /usr/bin/wp \
    && chown -R www-data:www-data /var/www/html/ \
    && /etc/init.d/mysql start \
    && mysql -e "CREATE DATABASE wordpress DEFAULT CHARACTER SET utf8;" -uroot -proot \
    && mysql -e "use wordpress;source /tmp/wordpress.sql;" -uroot -proot \
    && wp --allow-root --path=/var/www/html/ option set permalink_structure /archives/%post_id% \
    && rm -f /tmp/wordpress.sql

EXPOSE 80
CMD ["/start.sh"]

