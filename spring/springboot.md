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
### Step 1: pom.xml
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


### Step 2: Adding the bootstrap class
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


### Step 3: Running Spring Boot application using the Spring Tools IDE

1. Run the project with one of the three methods:

#### Manual Packaging and Running
- Package the Spring Boot application as a jar file using the integrated Maven tool in the 
terminal in the project directory:
```
% ./mvnw clean install
```
- Retrieve the jar file at `<project_directory>/target/<artifactId>-<version>.jar`
- Run on any machine with the required JRE version using:
```
% java -jar <jar_name>
```

#### Spring Boot Maven Plugin
In the terminal, in the project directory, use the Maven CLI:
```
./mvnw spring-boot:run
```

#### Spring Tools GUI
Go to Run menu -> Run As -> Java Application

2. See the Spring ASCII art appears on the console, along with Tomcat and the application
started. 
3. Check http://localhost:8080 (default port for Tomcat) to see Whitelabel Error Page because 
the `/error` has not been set up yet. In the console, it will show 
```
2025-10-14T23:16:56.675+07:00  INFO 3376 --- [nio-8080-exec-1] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring DispatcherServlet 'dispatcherServlet'
2025-10-14T23:16:56.675+07:00  INFO 3376 --- [nio-8080-exec-1] o.s.web.servlet.DispatcherServlet        : Initializing Servlet 'dispatcherServlet'
2025-10-14T23:16:56.677+07:00  INFO 3376 --- [nio-8080-exec-1] o.s.web.servlet.DispatcherServlet        : Completed initialization in 2 ms
```

## Ways to start a Spring Boot application
1. ### Spring Initializr 
    A webpage for fast setting up Spring Boot application at [start.spring.io](https://start.spring.io)<p>
    In Spring Tools, go to File -> Import -> Maven -> Existing Maven Projects -> browse to unzipped, generated project file
    
    #### Result Included: 
    1.1 Bootstrap class (as in step 2 earlier)<p>
    1.2 mvnw, mvnw.cmd - integrated Maven tool<p>
    1.3 parent: spring-boot-starter-parent (as in step 1 earlier)<p>
    1.4 properties: <java.version>21</java.version><p>
    1.5 dependency: spring-boot-starter-test<p>
    1.6 plugin: spring-boot-maven-plugin<p>


2. ### Spring Boot CLI:
    A Spring Boot command line tool documented at [spring-boot/cli](https://docs.spring.io/spring-boot/cli/index.html)
   
    #### Manual Installation Steps
    2.1 Download tar.gz from the official page: 
    ```
    % cd ~/opt
    % curl --output spring-boot-cli.tar.gz --location https://repo.maven.apache.org/maven2/org/springframework/boot/spring-boot-cli/3.5.6/spring-boot-cli-3.5.6-bin.tar.gz
    ```
    2.2 Extract the `spring-boot-cli.tar.gz` using this command:
    ```
    % tar -xvzf spring-boot-cli.tar.gz
    ```
    The folder should look like this:
    ```
    spring-3.5.6
    ├── INSTALL.txt
    ├── LICENCE.txt
    ├── bin
    │   ├── spring
    │   └── spring.bat
    ├── legal
    │   └── open_source_licenses.txt
    ├── lib
    │   └── spring-boot-cli-3.5.6.jar
    └── shell-completion
    ├── bash
    │   └── spring
    └── zsh
    └── _spring
    ```
    2.3 Even though the INSTALL.TXT says that we don't need to set the environment variable, 
    it seems like I do. 
    ```
    % cat opt/spring-3.5.6/INSTALL.txt
   
     ...
   
    Environment Variables
    ---------------------
    No specific environment variables are required to run the CLI, however, you may want to
    set SPRING_HOME to point to a specific installation. You should also add SPRING_HOME/bin
    to your PATH environment variable. 
    ```
    Follow these steps for successful installation.
    ```
    % nano ~/.zshrc
    
    // Modify the config file after maven_setup.md tutorial
    export JAVA_HOME="$HOME/opt/jdk-21.0.7/Contents/Home"
    export MAVEN_HOME="$HOME/opt/apache-maven-3.9.10"
    export SPRING_HOME="$HOME/opt/spring-3.5.6"
    export PATH="$JAVA_HOME/bin:$MAVEN_HOME/bin:$SPRING_HOME/bin:$PATH"
    
    // Save the file and exit
    [Ctrl] + [O]
    [Return]
    [Ctrl] + [X]
    ```
    2.4 Start a new shell (`cmd + N`) and check:
    ```
    ~ % echo $SPRING_HOME
    /Users/ratchapong/opt/spring-3.5.6
   
    ~ % which spring
    /Users/ratchapong/opt/spring-3.5.6/bin/spring

    ~ % spring --version
    Spring CLI v3.5.6
    ```
   
    #### Example
    Initialize a Java project into a Tennis directory (non-existing) with the following specifications:

    - language = Java
    - Spring Boot version = 3.5.6
    - packaging = jar
    - build = maven
    - artifactId = tennis
    - groupId = com.ryoma
    - version = 1.0.0
    - dependencies = spring-boot-starter-web, spring-boot-starter-data-jpa 

    with the Spring CLI as:
    ```
    % spring init -a tennis -g com.ryoma -v 1.0.0 -j 21 -l java -p jar -b 3.5.6 --build maven -d=web,jpa Tennis
    ```
   
    #### Result Included:
    1.1 Bootstrap class at `Tennis/src/main/java/com/ryoma/tennis/DemoApplication.java`<p>
    1.2 mvnw, mvnw.cmd<p>
    1.3 parent: spring-boot-starter-parent<p>
    1.4 properties: <java.version>21</java.version><p>
    1.5 dependencies: spring-boot-starter-test, spring-boot-starter-web, spring-boot-starter-data-jpa<p>
    1.6 plugin: spring-boot-maven-plugin<p>
    with the following project's information in pom.xml:
    ```
    <groupId>com.ryoma</groupId>
    <artifactId>tennis</artifactId>
    <version>1.0.0</version>
    <name>demo</name>
    <description>Demo project for Spring Boot</description>
    ```
   
3. ### STS IDE
    The most simple way if Spring Tools IDE is available.<p>
    Go with: File -> New -> Spring Starter Project -> edit specifications as in the former two ways<p>
    Then, the project is created, opened in Package Explorer, and ready for development in the IDE
