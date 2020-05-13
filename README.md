Docker and docker-compose class
===============================

Note about working user variables: you should export two variables at host machine — `DUID` (docker user id), variable with your current user ID and `DGID` (docker group id), variable with your current group.

These variables are uses for launch php-process in a container.

For example:    
```shell script
export DUID=$(id -u) && export DGID=$(id -g)
```

## Run project locally

1. Build project: 
    ```shell script
    docker-compose build
    ```
1. Launch project:
    ```shell script
    docker-compose up -d
    ```
1. Install packages:
    ```shell script
    docker-compose exec app composer install
    ```
1. Run tests:
    ```shell script
    docker-compose exec app vendor/bin/phpunit
    ```
