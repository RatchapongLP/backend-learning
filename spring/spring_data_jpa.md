# Spring Data JPA

## JPA (Java Persistence API)
- A specification for Object-Relational Mapping (ORM)
- Requires an implementation (like Hibernate or EclipseLink) to function.
- A core part of Java EE (Enterprise Edition) and Jakarta EE platforms, 
but can also be used in Java SE (Standard Edition) environments.

### JPA Annotations
- `@Entity`: used at DTO classes that are to be mapped to tables in relational databases
- `@Id`: used at DTO fields that are mapped to primary-keys in tables

## Spring Data JPA 
- Enables out-of-the-box repository class creation. No need for implementing basic CRUD methods.
- Have an interface implementing a common JPA implementation - CrudRepository<T, ID>, which 
contains basic CRUD operations. For example:
```
import org.springframework.data.repository.CrudRepository;

public interface TopicRepository extends CrudRepository<Topic, String> {}	
```

### CrudRepository vs JpaRepository
See this Stack Overflow [thread](https://stackoverflow.com/questions/34702252/spring-data-jpa-crudrepository-returns-iterable-is-it-ok-to-cast-this-to-list) for information.

## Apache Derby Database
- Open-source relational DBMS
- Entirely implemented in Java
- Supports embedded and client/server modes: 
  - **Embedded Mode:** Derby runs within the same Java Virtual Machine (JVM) as the application.
  - **Client/Server Mode:** Derby operates as a network server, allowing multiple clients to connect
  over a network using the Derby Network Server and Derby Network Client JDBC driver.

### Auto-detect in Spring Boot
Spring Boot can see the derby dependencies in the classpath from:
```
<dependency>
    <groupId>org.apache.derby</groupId>
    <artifactId>derby</artifactId>
    <scope>runtime</scope>
</dependency>
<dependency>
    <groupId>org.apache.derby</groupId>
    <artifactId>derbytools</artifactId>
    <scope>runtime</scope>
</dependency>
```
So it picks the derby as the database and autoconfigures an embedded database instance at runtime. 
No explicit connection URLs are required in application.properties for the basic embedded setup.
