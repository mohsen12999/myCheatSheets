# Spring Boot

## Requirement

- IDE: `intellij idea`
- documentation: [Ascii Doc](https://asciidoc.org/)

## Create Initial Project

- can make spring boot project with [spring initializr](https://start.spring.io/) or intellij idea wizard.
- add package:
  - Core:`Dev Tools`, `Lombok`.
  - Web: `Web`.
  - Template Engine: `Thymeleaf`.
  - SQL: `JPA`, `H2`.
  - Ops: `Actuator`.
- test app with `curl -i http://localhost:8080`

## Spring Boot Essentials

### Config Devtool

- for rebuild when code changing in intellij:
  - File -> Setting -> Build, Execution,Deployment -> Compiler -> check `Build project automatically`
  - File -> Setting -> Advance Setting -> check `Allow auto-make to start even if developer application is currently running` 
- more info: [Spring Boot Developer tools](https://docs.spring.io/spring-boot/docs/1.5.16.RELEASE/reference/html/using-boot-devtools.html)

### Configuration

- change setting in `src/main/resource/application.properties` like `spring.devtools.restart.enabled=false` or `server.port=8085`
- change define property of package there.

### Profiles

- can define active profile in `src/main/resource/application.properties`: `spring.profiles.active=test,dev`
- use with `@Profile('dev')`
- can define properties for difference profile like for `dev` -> `application-dev.properties`

### Debugging & Logging

- change logging level to show more log in `application.properties` with `logging.level.root=TRACE`.
- can change log level for one package `logging.level.com.mohsen.springit=DEBUG`.
- can change log file and other things too.
- for logging can use `org.slf4j` lib.

```java
// define
private static final Logger log = LoggerFactory.getLogger(SpringitApplication.class);

// use
log.error("we have error");
log.warn("keep watching");
log.info("we are here!");

log.debug('show when in debug or trace level');
log.trace('show only when in trace level');
```

## Actuator

- default in `/actuator`, change with `management.endpoint.web.base-path=/manage`
- `curl http://localhost:8080/actuator/env -i -X GET` or typing `http://localhost:8080/actuator/env` in browser to get information about your environment
- for get info in actuator, add this line in `application.properties`: `management.endpoint.health.show-details=always`
- add application info in `application.properties`
  - `management.application.name=Springit`
  - `management.application.desccription=Reddit clone using Spring Boot 2`
  - `management.application.version=0.0.1`
- show all available endpoint `management.endpoint.web.exposure.include=*`

## MVC

### Model

- use JPA (java persistence package) or `javax.persistence` package for making database model.
- `@Entity` before class name for show it is class.
- `@Id` for show properties is primary key.
- `@GenerateValue` making field auto generate value.
- `@Column(name="", nullable=false, length=512)` for string fields.
- `@Transient` field not save in database.
- more info in [Java Persistence](https://docs.oracle.com/javaee/7/api/javax/persistence/package-summary.html)

- most add constructor, setter and getter for all field and override toString, equal and hash code.
- can use [`Project Lombok`](https://projectlombok.org/) to make this code for us.
- must enable `annotation processing` in setting of editor.
- `@NoArgsConstructor` to make constructor without argument.
- `@NonNull`: field is not nullable.
- `@Data`: A shortcut for @ToString, @EqualsAndHashCode, @Getter on all fields, and @Setter on all non-final fields, and @RequiredArgsConstructor!

- repository, can choose between crud, paging and sorting and jpa repository. jpa repository extended from both crud and paging and sorting repository.

### Query Methods

- define method for using in application mor info [query methods](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#repositories.query-methods).

### Relation and Mapping

- [oneToMany doc](https://docs.oracle.com/javaee/7/api/javax/persistence/OneToMany.html)
- good article [Map Associations with JPA and Hibernate – The Ultimate Guide](https://thorben-janssen.com/ultimate-guide-association-mappings-jpa-hibernate/)

### Auditing

- add meta data with [Auditing](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#auditing)

## Database

- [common properties](https://docs.spring.io/spring-boot/docs/1.1.6.RELEASE/reference/html/common-application-properties.html)

- enable h2 console in `application.properties` with: `spring.h2.console.enabled=true`, after that we can see h2 properties in '/h2-console'

### use MySQL

- need to add `mysql` dependency

```xml
<dependency>
  <groupId>mysql</groupId>
  <artifactId>mysql-connector-java</artifactId>
</dependency>
```

- `spring.jpa.hibernate.ddl-auto=create` -> drop and create table every time
- database url: `spring.datasource.url=jdbc:mysql://localhost:3306/springit?useSSL=false`
- database user and password: `spring.datasource.username=root`, `spring.datasource.password=`

### Command line Runner

- Interface used to indicate that a bean should run when it is contained within a SpringApplication.
- if we define a class we must use `@Component` to tag class.
- use `ApplicationRunner` when we need application args.
- can have multiple and order them with `@Order([order-number])`
- use `@Bean` for define command line function in application class.

## Reference

- [Getting Started with Spring Boot 2](https://www.udemy.com/course/spring-boot-2/) by [Dan Vega](https://www.danvega.dev/)
- [course doc](https://www.danvega.dev/docs/spring-boot-2-docs/)
