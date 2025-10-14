# Spring Boot
## What is Spring Boot?
It comprises of two things: Spring and Boot. So let understand Spring first.

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

## Spring Tools for Eclipse (Version: 4.32.0.RELEASE)
### Initial setups for JavaSE-21
1. Preferences -> Java -> Installed JREs -> Execution Environments -> JavaSE-21 on the left and JRE [21.0.8] [perfect match] 
-> Apply and Close
2. Preferences -> Java -> Installed JREs -> Select JRE [21.0.8] (default) -> Apply -> Apply and Close
3. Package Explorer -> right-click the project directory -> Build Path -> Java Build Path -> Libraries -> delete the old JRE 
-> Add Library -> JRE System Library -> Workspace default JRE (JRE [21.0.8]) -> Finish
4. Package Explorer -> right-click the project directory -> Build Path -> Java Compiler -> Choose a drop down option
of "Compiler compliance level" to 21 -> Apply -> Apply and Close
5. Package Explorer -> right-click the project directory -> Properties -> Resource ->
Text file encoding -> select Other: -> choose UTF-8 from the dropdown menu -> Apply and Close

## Steps to apply Spring Boot to a maven project
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
