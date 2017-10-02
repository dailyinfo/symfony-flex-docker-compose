### Setup

1. Place a Symfony 3.4+/4 app in `$PROJECT_ROOT/app` (create a new Symfony Flex project with `composer create-project symfony/skeleton app`)
2. Change your `app/.env` file to match the database settings from `docker-compose.yml`
3. `docker-compose up -d`

### Includes

* nginx/PHP7.1
* MariaDB
* Composer
* Elasticsearch
* Redis
* ELK stack for logs (Elasticsearch, Logstash, Kibana)

### Running commands

Symfony commands can be run using the symfony container, e.g.

`docker-compose run symfony bin/console debug:router`

It will save time if you set up an alias within your shell for `docker-compose run symfony bin/console`.

### Using Composer

Composer commands can be run within the symfony container:

`docker-compose run symfony composer *command*`

### Using other services

**Elasticsearch** elasticsearch:9200  
**Redis** redis:5379  
(from other containers - ports also exposed on host machine)

View logs in Kibana at localhost:8080

### Hosts file

Add an entry to your hosts file to be able to access your app from `http://symfony.dev`. `http://localhost` works too.

127.0.0.1 symfony.dev