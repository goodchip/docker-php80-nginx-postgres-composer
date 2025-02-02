# docker-php8-GD-library-nginx-postgres-composer

Docker Compose configuration to run PHP8 (including GD-Library) with Nginx, PHP-FPM, PostgreSQL 10.1 and Composer.

## How to use it

### Starting Docker Compose

```
docker-compose up -d
```

### Using Composer

`docker-compose run --rm composer <cmd>`

Where `cmd` is any of the available composer command.

### Using PostgreSQL

Default connection:

`docker-compose exec db psql -U postgres`

Using .env file default parameters:

`docker-compose exec db psql -U db_user db_name`

### Using PHP

You can execute any command on the `php` container as you would do on any docker-compose container:

`docker-compose exec php php --version`

for example, when you run test,

`docker-compose exec php php vendor/bin/phpunit`

#### Test your development environment with phpunit

`docker-compose exec php vendor/bin/phpunit ./tests`

```
PHPUnit 9.5.4 by Sebastian Bergmann and contributors.

..                                                                  2 / 2 (100%)

Time: 00:00.022, Memory: 4.00 MB

OK (2 tests, 2 assertions)
```

## Change configuration

### Configuring PHP

To change PHP's configuration edit `.docker/conf/php/php.ini`.

You can add any .ini file in this directory, don't forget to map them by adding a new line in the php's `volume` section of the `docker-compose.yml` file.

### Configuring PostgreSQL

Any .sh or .sql file you add in `./.docker/conf/postgres` will be automatically loaded at boot time.

If you want to change the db name, db user and db password simply edit the `.env` file at the project's root.

If you connect to PostgreSQL from localhost a password is not required however from another container you will have to supply it.

## install to your project

```
cp -r .env .docker/ docker-compose.yml /path/to/your/project
```

## Development

```
$ ./test-install-script.sh 
ARGUMENTS ERROR: dir not set
ARGUMENTS ERROR: dir not exists
total 20
drwxrwxr-x 3 taro taro 4096 Sep 12 01:50 .
drwxrwxr-x 6 taro taro 4096 Sep 12 01:50 ..
drwxrwxr-x 3 taro taro 4096 Sep 12 01:50 .docker
-rw-rw-r-- 1 taro taro  965 Sep 12 01:50 docker-compose.yml
-rw-rw-r-- 1 taro taro   56 Sep 12 01:50 .env
```



