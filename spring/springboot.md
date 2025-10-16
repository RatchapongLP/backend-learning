# Spring Boot
## What is Spring Boot?
It comprises two things: Spring and Boot. So let understand Spring first.

### Spring in a nutshell
Spring (without Boot) is a multi-purpose framework
for enterprise-level applications. It offers tons of functionality other than "dependency injection", e.g., 
handling databases transaction management, authentication and authorization features, etc. 
It simplifies many boilerplate code and complex configurations originally found when 
developing using Java EE. 

### Boot part of Spring Boot
Spring Boot further abstracts the existing configuration that the majority (roughly 80% according to Kushik, Java Brains)
of developers already adopting as a "convention" to an even more out-of-the-box version. It helps "bootstrapping"
Spring applications to another level. For instance, a web container is bundled in the application so that the final jar 
acts as a stand-alone app, no need for additional server to run and deploy the war files. Also, the dependencies are bundled
as various groups called 'meta' or 'parent' dependencies to allow more convenient development.

## Steps to apply Spring Boot to a maven web application project 
### pom.xml
1. Under `<project>`, add the Spring Boot starter as the project parent, enabling it to inherit 
'opinionated' maven configurations from the parent:
```
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>4.0.0-M3</version>
</parent>
```
2. Under `<project>`, configure as JavaSE-21: 
```
  <properties>
  	<java.version>21</java.version>
  </properties>
```
Then save -> right click the project directory in the explorer -> Maven -> Update Project...
See that the version trailing the 'JRE System Library' has changed from [JavaSE-17] to [JavaSE-21].
This overrides the default version of the parent's maven configuration.

3. Add the Spring Boot web's starter dependency, which includes Spring MVC, Tomcat, etc.
```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```
`spring-boot-starter-web` contains spring web dependencies (including spring-boot-starter-tomcat):
- `spring-boot-starter`
- `jackson`
- `spring-core`
- `spring-mvc`
- `spring-boot-starter-tomcat`

`spring-boot-starter-tomcat` contains everything related to an embedded tomcat server:
- `core`
- `el`
- `logging`
- `websocket`

**Note:** the Tomcat configurations that we usually need to do when running the servlet container 
are already set and done by Spring Boot in merge with 'application configuration'.

> ***Bill of Materials***<br>
The dependencies here tell Maven which jars to download, but the version of the jars are specified and 
configured by the parent.
Spring Boot calls it "Bill of Materials", meaning that we don't have to worry about jars versions compatibilities.
just pick the version of the parent or combination, all the components jars have already been checked 
and approved that they work well together.



### Setting up JavaSE-21 in Spring Tools for Eclipse (Version: 4.32.0.RELEASE) 
See **JRE 21 setting** in [java-environment/spring_tools.md](../java-environment/spring_tools.md)

### Adding the bootstrap class
1. Create a class with a `public static void main(String[] args)` method.
2. Annotate the class with `@SpringBootApplication` to enable the class as the starting point.
3. In the `main` method, add the following statement:
```
SpringApplication.run(<class_name_from_step_1.>.class, args);
```
This class will bootstrap the application: 
- sets up the 'convention' or default configuration.
- creates a Spring application context (which scans for markers in the
classpath: business, controller, services, dao, etc.) 
- runs the servlet container .
- hosts the app at the default port.

### Running Spring Boot application using the Spring Tools IDE
1. Run the project in Spring Tools as Java application
2. See the Spring ASCII art appears on the console, along with Tomcat and the application
started. 
3. Check http://localhost:8080 (default port for Tomcat) to see Whitelabel Error Page because 
the `/error` has not been set up yet. In the console, it will show 
```
2025-10-14T23:16:56.675+07:00  INFO 3376 --- [nio-8080-exec-1] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring DispatcherServlet 'dispatcherServlet'
2025-10-14T23:16:56.675+07:00  INFO 3376 --- [nio-8080-exec-1] o.s.web.servlet.DispatcherServlet        : Initializing Servlet 'dispatcherServlet'
2025-10-14T23:16:56.677+07:00  INFO 3376 --- [nio-8080-exec-1] o.s.web.servlet.DispatcherServlet        : Completed initialization in 2 ms
```

## Adding a controller
A class that contains methods that will be execute when certain URL accesses are called to the application.
In Spring (Spring MVC), the class has to be annotated with `@Controller`


