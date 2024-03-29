# Laravel Docker
## Powered By [InfancyIT](https://www.infancyit.com)
------------------------------------------------------
# Documentation

## Run

    docker-compose up

## Container List
Name | Conatiner | Version
-----|----------|-----------
`nginx` | Nginx | 1.16.0 
`php7` | PHP | 7.3
`php5` | PHP | 5.6
`mysql` | MySQL | 5.7.22
`phpmyadmin` | PhpMyAdmin | -

## Add new project

1. Clone/Copy the project folder inside `./src` 
    -  Run neccesary comands
         - `composer update`
         - `cp .env.example .env`
    - If your native OS doesn't have `composer` or `php` you can run any command from inside container by selecting the proper container:
       - `docker-compose exec php7 {your_command}`
       - `docker-compose exec php5 {your_command}`
       - `docker-compose exec php7 bash -c "cd {folder_name} && composer update"`
2. Now we will create a `.conf` file for nginx.
    - Copy `./nginx/conf/sites-enabled/default.conf` to a new `conf` file
    - Edit the followinng peroperty
        - `server_name` on `line 3`
        - `port` on `line 4`
            - If you have a domain you have to select port 80
            - If you don't have any domain you can listen to any port from 8000-8100 range
            - You can listen multiple port for a single project also
        - `root` on `line 6`. Here you have to put the path of the `index.php`/`index.html` of the project and `./src` should be replaced by `/var/www/`
            - eg: For a traditional laravel project named `laravel_test_infancy` inside `./src`, the `root` should be `/var/www/laravel_test_infancy/public`
            - eg: For a traditional vuejs project named `vuejs_test_infancy` inside `./src`, the `root` should be `/var/www/vuejs_test_infancy/dist`
        - `fastcgi_pass` on `line 22`
            - If you need `php 5.6` put `php5:9001`
            - If you need `php 7.3` put `php7:9000`
3. To create a database you can access `PhpMyAdmin` on port `50` by default,
alternatively you can create database via `docker-compose exec` from the root of this repository or manually putting database name on `docker-compose.yml` file
4. If your project has a `.env` update it as:
    - `DB_HOST=db`
    - `DB_PASSWORD={as per as this repo .env file}`
5. To run migration and/or necessary `artisan` command, you can:
    - `docker-compose exec php5 php {project_name}/artisan migrate --seed`
    - `docker-compose exec php7 php {project_name}/artisan migrate --seed`
6. To set the folder permissions for the container you should run:
    - For laravel 4.2 `docker-compose exec php5 chmod 777 -R  {project_name}/app/storage`
    - For laravel 5.\*/6.\* `docker-compose exec php7 chmod 777 -R  {project_name}/storage`
7. And finally:
    - `docker-compose restart`
    - or `docker-compose down && docker-compose up`