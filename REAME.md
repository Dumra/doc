# Smeetz Docker

This [Docker Compose] powered development environment includes:

  * PHP 7.2 FPM container with Smeetz backend app, CLI tools, and Xdebug
  * Nginx web server, serving smeetz api
  * MySQL database
  * Composer


## Installation

Docker Platform can be installed on Windows, Mac, or Linux from [their website](https://www.docker.com/products/overview).   
Install [Docker](https://docs.docker.com/install/).  
Install [Docker Compose](https://docs.docker.com/compose/install/).  
Once installed it will run as a background process, and the versions can be checked at the command line:

```
$ docker -v
$ docker-compose -v
```

### Cloning the backend repo

```
# Clone this repository for set up docker env
$ git clone https://<username>@bitbucket.org/Smeetz/smeetz-backend.git,

where <username> ur nickname on bitbucket.

```

### Configuring the environment

The [.env.dist](./.env.dist) file found in the root folder should be copied to `.env`, which is ignored by Git.  
Don't forget to change config files of smeetz-backend app (`.env` file) with new database path if you're going to migrate database from host machine. 

```
# Copy default environment settings
$ cp .env.dist .env
```

### Running the environment

**Running docker containers**
```
# Run the environment, ctrl+c to shutdown
$ docker-compose up

# Or run in detached mode with -d, and shutdown after
$  docker-compose  up -d
$ docker-compose down

# To rebuild containers after changes to Docker configuration
$  docker-compose  up --build

# Interact with container
$ docker exec -it -u $(id -u):$(id -g) CONTAINER_NAME bash
```

_If there are no changes to Docker configuration then running `docker-composer up --build` with the build flag takes very little extra time._

**Running Smeetz backend.**

```bash
#Docker docker containers name/ids
$ docker ps
# Interact with container with current user (working only on Unix OS) or
$ docker exec -it -u $(id -u):$(id -g) CONTAINER_NAME bash
# Interact with container
$ docker exec -it CONTAINER_NAME bash
# Run composer
$ composer install
# Create db
$ php bin/console doctrine:database:create
# Compute difference from old database to new database
$ php bin/console doctrine:schema:update --dump-sql
# Force the changes on the database
$ php bin/console doctrine:schema:update --force
# Load data into the database
$ php app/console doctrine:fixture:load

```

Also, please add this domain to ur local host file
```
api.smeetz.local
```