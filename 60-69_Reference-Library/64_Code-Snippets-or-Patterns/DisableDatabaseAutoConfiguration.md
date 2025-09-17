---
id: DisableDatabaseAutoConfiguration
aliases: []
tags:
  - code-snippet
  - spring-boot
---

# Code Snippet - DisableDatabaseAutoConfiguration

## Description

### Purpose

This snippet will disable all database related configuration. The Application
shouldn't try to establish a connection with the database once this explicitly
included to the root file.

### Context

An application where it won't use a database as a server or data persistence.

## Code

### Using Annotations

```java
@SpringBootApplication
@EnableAutoConfiguration(exclude = {
    DataSourceAutoConfiguration.class,
    DataSourceTransactionManagerAutoConfiguration.class,
    HibernateJpaAutoConfiguration.class})
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(PayPalApplication.class, args);
    }
}
```

### Using application.properties

```properties
spring.autoconfigure.exclude=org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration,org.springframework.boot.autoconfigure.orm.jpa.HibernateJpaAutoConfiguration
```

### Using application.yml

```yml
spring:
  autoconfigure:
    exclude:
      - org.springframework.boot.autoconfigure.orm.jpa.HibernateJpaAutoConfiguration
      - org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration
```
