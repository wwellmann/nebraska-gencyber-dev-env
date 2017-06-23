# nebraska-gencyber-dev-env
This repository provides a central location that contains sub-modules related to the programmatic environment for the Nebraska GenCyber Camp

### Requirements
* Docker (https://www.docker.com/)

### Installation
You need to build the docker image from the provided DockerFile and Docker Compose. To do this, ensure docker is running, and then:

```bash
git clone --recursive https://github.com/MLHale/nebraska-gencyber-dev-env.git
cd nebraska-gencyber-dev-env
docker-compose build
```

This creates a few docker containers with all of the requisite installed dependencies to run the dev environment.

### Setup
First, upon initial install, you need to do some basic setup.

#### Django
We need to initialize the Django database in postgres

```bash
docker-compose run django bash
python manage.py makemigrations
python manage.py migrate
python manage.py createsuperuser --username admin --email admin
```
Now specify a password for admin. In development, use admin1234 for simplicity.

### Backing up and restoring database from Postgres
You can export data from postgres using the script:

#### Backup
```bash
docker-compose run db pg_dump -U postgres postgres | gzip > database-backup/backupfile-name.gz
```

#### Restore
```bash
docker-compose run db pg_dump -U postgres postgres | gzip > database-backup/restorefile-name.gz
```
