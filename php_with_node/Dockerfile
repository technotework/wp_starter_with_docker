FROM php
RUN cd ~
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('sha384', 'composer-setup.php') === 'c31c1e292ad7be5f49291169c0ac8f683499edddcfd4e42232982d0fd193004208a58ff6f353fde0012d35fdd72bc394') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php --install-dir=/usr/local/bin --filename=composer
RUN php -r "unlink('composer-setup.php');"
RUN composer -V
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -
RUN apt-get install -y nodejs
RUN apt-get install -y git
RUN apt-get install -y zip unzip
RUN composer global require "squizlabs/php_codesniffer=3.*"
ENV PATH $PATH:/root/.composer/vendor/bin
RUN echo $PATH
RUN composer global require wp-coding-standards/wpcs
RUN composer global require wptrt/wpthemereview
RUN phpcs --config-set installed_paths /root/.composer/vendor/wp-coding-standards/wpcs,/root/.composer/vendor/wptrt/wpthemereview/WPThemeReview 
RUN phpcs -i