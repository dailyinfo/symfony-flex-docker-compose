### Setup

1. Copy `.env.dist` to `.env` and edit the path to your Symfony app, and the database parameters (will need to match your database parameters in your Symfony app's config)
3. `docker-compose up -d`

### Includes

* nginx/PHP7.1
* MariaDB
* Composer
* ELK stack for logs (Elasticsearch, Logstash, Kibana)

### Running commands

Symfony commands can be run from the **php** container, e.g.

```
docker-compose exec php bin/console app:my_command
```

It will save time if you set up an alias within your shell for `docker-compose exec php bin/console`.

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

Composer commands can be run within the **php** container:

`docker-compose exec php composer *command*`

### Logs

View logs in Kibana at localhost:8080

### Hosts file

Add an entry to your hosts file to be able to access your app from `http://symfony.dev`. `http://localhost` works too.

127.0.0.1 symfony.dev