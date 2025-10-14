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
as various groups to allow more convenient development.

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

