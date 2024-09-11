# run

## spring-boot:run

```bash
./mvnw spring-boot:run -Dspring-boot.run.jvmArguments="-Dspring.profiles.active=testdata"
```

## jar(cli arguments)

```bash
java -jar target/catalog-service-0.0.1-SNAPSHOT.jar --polar.greeting="Welcome to the catalog from CLI"
```
```bash
java -jar target/catalog-service-0.0.1-SNAPSHOT.jar --spring.profiles.active=prod
```

## jar(vm properties)

```bash
java -Dpolar.greeting="Welcome to the Catalog form JVM" -jar target/catalog-service-0.0.1-SNAPSHOT.jar
```

jvm 속성과 cli 인자를 둘 다 주면 우선 순위에 따라 cli 인자가 적용된다.

```bash
java -Dpolar.greeting="Welcome to the Catalog form JVM" -jar target/catalog-service-0.0.1-SNAPSHOT.jar --polar.greeting="Welcome to the catalog from CLI"
```

## jar(system properties)

```bash
POLAR_GREETING="Welcome to the catalog from ENV" java -jar target/catalog-service-0.0.1-SNAPSHOT.jar
```

```powershell
$env:POLAR_GRETTING="Welcome to the catalog from ENV"; java -jar target/catalog-service-0.0.1-SNAPSHOT.jar
```
```powershell
Remove-Item Env:POLAR_GREETING
```

# test

```bash
./mvnw test -Dtest="BookRepositoryJdbcTests"
```

# refresh

```bash
http POST :9001/actuator/refresh
```




# postgresql

## start/stop

```bash
docker run -d \
    --name polar-postgres \
    -e POSTGRES_USER=user \
    -e POSTGRES_PASSWORD=password \
    -e POSTGRES_DB=polardb_catalog \
    -p 5432:5432 \
    postgres:16.3
```

```bash
docker rm -fv polar-postgres
```

## database commands

```bash
docker exec -it polar-postgres psql -U user -d polardb_catalog
```

`\list`
`\connect polardb_catalog`
`\dt`
`\d book`
`\quit`

# docker

```bash
./mvnw spring-boot:build-image
```

```bash
docker network create catalog-network
```

```bash
docker run -d \
    --name polar-postgres \
    --net catalog-network \
    -e POSTGRES_USER=user \
    -e POSTGRES_PASSWORD=password \
    -e POSTGRES_DB=polardb_catalog \
    -p 5432:5432 \
    postgres:16.3
```

```bash
docker run -d \
    --name catalog-service \
    --net catalog-network \
    -p 9001:9001 \
    -e SPRING_DATASOURCE_URL=jdbc:postgresql://polar-postgres:5432/polardb_catalog \
    -e SPRING_PROFILES_ACTIVE=testdata \
    catalog-service
```

```bash
./mvnw spring-boot:build-image \
    -Dspring-boot.build-image.imageName=ghcr.io/{account}/catalog-service \
    -Dspring-boot.build-image.publish=true \
    -DregistryUrl=ghcr.io \
    -DregistryUsername={account} \
    -DregistryToken={github personal access token}
```
