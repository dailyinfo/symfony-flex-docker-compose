A minimum-hassle docker-compose setup for developing Symfony Flex applications.

### Includes

* nginx/PHP7.1
* MySQL (or MariaDB)
* Composer
* ELK stack for logs (Elasticsearch, Logstash, Kibana)

### Setup

1. Copy `.env.dist` to `.env` and edit the path to your Symfony app, and the database parameters (will need to match your database parameters in your Symfony app's config)
2. `docker-compose up -d`

If you would rather run MariaDB than MySQL, change the image of the database service in docker-compose.yml to your preferred MariaDB version (eg mariadb:10.3)

### Prerequisites

* [Docker](https://www.docker.com/get-docker)
* [docker-compose](https://docs.docker.com/compose/install/) (installed as part of Docker on Windows/Mac)

### Creating a new Symfony app

You can create a new Symfony Flex app using [Composer](https://getcomposer.org/):

```
composer create-project symfony/skeleton app
```

Replace *app* with the path (absolute or relative) to where you'd like the app directory to be created.

**Note:** The `composer` container cannot be used for creating the project, as it depends on mounting the `./app` directory. The container is meant to be used for running composer commands within the context of your project.

### Running commands

Symfony commands can be run from the **php** container, e.g.

```
docker-compose exec php bin/console app:my_command
```

It will save time if you set up an alias within your shell for `docker-compose exec php bin/console`.

### xDebug

To enable xDebug step-debugging within commands, you need to set the *xdebug.remote_host* PHP directive - on the command line like so:

```
docker-compose exec php php -dxdebug.remote_host=192.168.1.2 bin/console app:my_command
```

Replace *192.168.1.2* with your **host** machine's local network IP. I have a bash alias set up for running commands that does this automatically:

```
alias dcrs="docker-compose exec php php -dxdebug.remote_host=$(ip route get 192.168.1.1 | awk '{print $NF; exit}') bin/console"
```

Replace *192.168.1.1* with your local network's gateway, or *8.8.8.8*.

### Using Composer

Composer commands can be run within the **composer** container:

`docker-compose exec composer *command*`

Sometimes dependencies or Composer scripts require the availability of certain PHP extensions. You can work around this as follows:

* Pass the --ignore-platform-reqs and --no-scripts flags

### Logs

View logs in Kibana at `http://localhost:8080`

### Hosts file

Add an entry to your hosts file to be able to access your app from `http://symfony.test`. `http://localhost` works too.

127.0.0.1 symfony.test
