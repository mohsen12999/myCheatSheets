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

## Reference

- [Getting Started with Spring Boot 2](https://www.udemy.com/course/spring-boot-2/) by [Dan Vega](https://www.danvega.dev/)
