# Postgresql 

### Stop local server on mac

```shell
brew services stop postgresql

```

### Run Postgres on Docker

```shell
docker run -d --name dev-postgres -e POSTGRES_PASSWORD=<PG_PASSWORD> -p 5432:5432 postgres

```