Composer
===
#### Instalar globalmente
```
$ curl -sS https://getcomposer.org/installer | php
$ mv composer.phar /usr/local/bin/composer
Para fedora, aws EC2
$ ln -s /usr/local/bin/composer /usr/bin/composer
```

Console
===
#### Instalar globalmente
```
Primero instalar composer, luego:
$ curl -LSs http://drupalconsole.com/installer | php
$ mv console.phar /usr/local/bin/drupal
$ ln -s /usr/local/bin/drupal /usr/bin/drupal
```

Drush para drupal 8
===
#### Instalar globalmente
```
Primero instalar composer, luego:
$ composer global require drush/drush:dev-master
$ git clone https://github.com/drush-ops/drush.git /usr/local/src/drush
$ cd /usr/local/src/drush
$ git checkout master-fulltest  #or whatever version you want.
$ ln -s /usr/local/src/drush/drush /usr/bin/drush
$ composer install
$ drush --version
```


Referencias
===
Composer
https://getcomposer.org/doc/00-intro.md#globally

Console
https://www.drupal.org/project/console

Drush
http://docs.drush.org/en/master/install/

