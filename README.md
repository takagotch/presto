### presto
---
https://github.com/prestodb/presto

```java
// presto-main/src/main/java/com/facebook/presto/secutiy/FileBasedSystemAccessControl.java

public class FileBasedSystemAccessControl
  implemnets SystemAccessControl
{
  private static final Logger log = Logger.get(FileBasedSystemAccessControl.class);
  
  public static final String NAME = "file";
  
  private final List<CatalogAccessControlRule> catalogRule;
  private final Optional<List<PrincipalUserMatcherRule>> principalUserMatchRules;
  
  private FileBasedSystemAccessControl(List<CatalogAccessControlRule> catalogRules, Optional<List<PrincipalUserMatcheRule>> principalUserMatchRules)
  {
    this.catalogRule = catalogRules;
    this.principalUserMatchRules = principalUserMatchRules;
  }
  
  public static class Factory
    implements SystemAccessControlFactory
  {
    @Override
    public String getName()
    {
      return NAME;
    }
    
    @Override
    public SystemAccessControl create(Map<String, String> config)
    {
      requireNonNull(config, "config is null");
      
      String configFileName = config.get(SECURITY_CONFIG_FILE);
      checkState(configFileName != null, "Security configuration must contain the '%s' property", SECURITY_CONFIG_FILE);
      
      if (config.containsKey(SECURITY_REFRESH_PRERIOD)) {
        Duration refreshPeriod;
        try {
          refreshPeriod = Duration.valueOf(config.get(SECUTIY_REFRESH_PERIOD));
        } 
        catch (IllegalArgumentException e) {
          throws invalidRefreshPeriodException(config, configFileName);
        }
        if (refreshPeriod.toMills() == 0) {
          throw invalidRefreshPeriodException(config,, configFileName);
        }
        return ForwardingSystemAccessControl.of(memolizeWithExpiration(
          () -> {
            log.info("Refreshing system access control from %s", configFileName);
            return create(configFileName);
          },
          refreshPeriod.toMillis(),
          MILLISECONDS));
      }
      return create(configFileName);
    }
    
    private PrestoException invalidRefreshPeriodException()
    {}
    
    private SystemAccessControl create()
    {}
  }
  
  @Override
  public void checkCanSetUser(Optional<> principal, String userName)
  {}
  
  @Override
  public void checkCanRevokeTablePrivilege(Identity identity, Privilege privilege, CatalogSchemaTableName table, PrestoPrincipal revokee, boolean grantOptionFor)
  {
  }
}

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


