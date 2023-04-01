# gockerpg
A dockerized api template with Go and postgresql

### Prerequisites

- Have Go installed locally and GOPATH configured
- Have Docker installed locally

### Launch containers
```shell
docker-compose up -d --build
```

### Run the server without docker
```shell
go run .
```

### Adding migrations to postgres

Create your migration file in `migrations/postgres/tables`

```shell
touch migrations/postgres/tables/sample.sql
```

In `migrations/postgres/deploy_schemas.sql`

Add lines for each desired table as follow
```sql
\i '/docker-entrypoint-initdb.d/tables/sample.sql'
```

In `migrations/postgres/Dockerfile`, uncomment these lines
```Dockerfile
ADD ./tables/ /docker-entrypoint-initdb.d/tables/
ADD deploy_schemas.sql /docker-entrypoint-initdb.d/
```
