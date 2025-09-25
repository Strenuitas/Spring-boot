# YAML/Properties 配置文件 = 一个大 Map

### key = "short-link.domain.default"

### value = "nurl.ink:8001"

### @Value = 去 Map 里取值




####  类似于这种
```java
short-link:
  domain:
    default: nurl.ink:8001
  stats:
    locale:
      amap-key: feac1e83c78a14a943174ed7e2a03a6c
mybatis-plus:
  configuration:
    log-impl: org.apache.ibatis.logging.stdout.StdOutImpl
  mapper-locations: classpath:mapper/*.xml
