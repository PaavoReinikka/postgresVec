# Docker services for Postgres + vector-extension and Flyway

A quick way to setup postgres for LLM/genAI applications that need a knowledge base with embeddings and fast vector search.

## Database persistence

To ensure database data is persisted locally (i.e., not lost when containers stopped or removed), './pgdata/ ' directory is bind mounted. The database creates the directory on initial run. You can also create it yourself:

```
mkdir -p ./pgdata # creates if not exist
chmod 700 ./pgdata # sets secure permissions (pg default)
sudo chown -R 999:999 ./pgdata # sets ownership to default pg user inside the container (UID 999)
```

**NOTE:**
If you change to a custom Postgres image or user, check the UID/GID with:

```
docker run --rm <root/image:version> id postgres
```

and adjust the `chown` accordingly.

(here root=reinikp2 and image=pgvector-database, version 1)

## Running 


```
docker compose up --build 
```

(no need to build repeatedly unless changes...)

And stopping:

```
docker compose down 
```

## Checking the containers, environment variable etc.

You can enter the running container with 

```
docker exec -it postgresql_database bash # or psql directly to check the database
```

Within the container, you might want to run `printenv` command to check the environment variables.


## Developing the client with Python

If you want to develop the client using Python and run it as a container, you should check [reinikp2/python-3.13-slim-uv](https://hub.docker.com/repository/docker/reinikp2/python-3.13-slim-uv/general)


from docker hub -- it's the standard 3.13 slim but has uv pre-configured.

## Data-preparation

This is just an empty scaffolding for ETL and all bulk data loading that can not be done in migrations (alone).

**data-preparation** has a minimal dockerfile, which has some default dependencies -- it is likely to change. If the ETL is done using Python, and the 3.13 slim is sufficient, that should be used as the base image.
