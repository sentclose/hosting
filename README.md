# Sentc api self-hosting

with docker.

Follow the steps to self-host the sentc api with docker compose.

1. Copy and rename the following files:
    - `.env.sample` -> `.env`
    - `sentc.env.sample` -> `sentc.env`
2. Create a Root key with the sentc key gen and put it in ROOT_KEY:
```bash:no-line-numbers
docker-compose -f key_gen/docker-compose.yml up
```
3. (optional but recommended) change mysql env in the .env file

## Mariadb

To start the mysql version:

```shell
docker-compose -f mysql/docker-compose.yml up -d
```

This will also create a mariadb container. If you have already a db use:

```shell
docker-compose -f mysql/docker-compose.external_db.yml up -d
```

Make sure the env: `MYSQL_HOST` for the mariadb host and `MYSQL_DB` for the mariadb database name are set.

To only start the services individual use:

```shell
docker-compose -f mysql/docker-compose.api.yml up -d
```

To start the api or:

```shell
docker-compose -f mysql/docker-compose.file_worker.yml up -d
```

to start the file background worker.

## Sqlite

Before to start make sure a sqlite db is already placed into the directory: `db/sqlite`. 
You can use the db from the sentc-api repository. This dir will be a mounted volume into the docker container.

```shell
docker-compose -f sqlite/docker-compose.yml up -d
```