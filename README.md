### presto
---
https://github.com/prestodb/presto

```
```

```sh
./mvnw clean install
./mvnw clean install -DskipTests
shh -h -N -D 1080 server
-Dhive.metastore.thrit.client.sockes-proxy=localhost:1080
presto-cli/target/presto-cli-*-executable.jar
SELECT * FROM system.runtime.nodes;
SHOW TABLE FROM hive.default;
yarn --cwd presto-main/src/main/resources/webapp/src install
yarn --cwd presto-main/src/main/resource/webapp/src run package
yarn --cwd presto-main/src/main/resource/webapp/src run watch
```

```
```


