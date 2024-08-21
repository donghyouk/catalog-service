# run

## spring-boot:run

```bash
./mvnw spring-boot:run -Dspring-boot.run.jvmArguments="-Dspring.profiles.active=testdata"
```

## jar(cli arguments)

```bash
jara -jar target/catalog-service-0.0.1-SNAPSHOT.jar --polar.greeting="Welcome to the catalog from CLI"
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
