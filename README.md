# Laravel Docker
## Powered By [InfancyIT](https://www.infancyit.com)
------------------------------------------------------
# Documentation

## Run

    `docker-compose up`

## Add new project to laravel

1. Clone/Copy the project folder inside `./var/www` 
    - You can run any command inside the container via 
   `docker-compose exec {container} {your_command}`
   
   If the project requires php7.0+ then you can run: 
    - eg: `docker-compose exec php_7.3 cd {project_name} && composer update`
    - eg: `docker-compose exec php_7.3 php {project_name}/artisan migrate --seed`
    
   If the project requires php5.6 then you can run: 
    - eg: `docker-compose exec php_5.6 cd {project_name} && composer update`
    - eg: `docker-compose exec php_5.6 php {project_name}/artisan migrate --seed`

2. 