# Docker by stacks

## Choose a stack

1. Open the file archi_list.yaml and choose a stack

2. Go the directory corresponding to the selected stack

## Install the stack

1. Create a `.env` from the `.env.dist` file. Adapt it according to your symfony application

    ```bash
    cp .env.dist .env
    ```

2. Build/run containers with (with and without detached mode)

    ```bash
    $ docker-compose build
    $ docker-compose up -d
    ```

## Find the docker machine ip

There are several ways to get the docker ip and I go through this way.

```bash
    # List all docker machines ip
    $ ip ad | grep "docker"

    # Find the good one

    # Note the ip
```

## Stack archi_php72_a:

1. Prepare the stack

    * Update app/config/parameters.yml

        ```yml
        # path/to/your/symfony-project/app/config/parameters.yml
        parameters:
            database_host: db
        ```

    * Composer install & create database

        ```bash
        $ docker-compose exec php bash
        $ composer install
        # Symfony
        $ sf (or sf3) doctrine:database:create
        $ sf (or sf3) doctrine:schema:update --force
        # Only if you have `doctrine/doctrine-fixtures-bundle` installed
        $ sf (or sf3) doctrine:fixtures:load --no-interaction
        ```

2. Use the stack

    * Symfony app
        + the_ip/app_dev.php (dev environment):
        + the_ip (prod environment)
    * PhpMyAdmin
        + the_ip:8080 (host: db, user: root, password: root)
        +
            ```bash
            $ docker-compose exec db mysql -uroot -p"root"
            ```
    * Logs files location
        + logs/nginx
        + logs/symfony
