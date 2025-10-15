# Spring Tools for Eclipse (Version: 4.32.0.RELEASE)

## JRE 21 setting
1. Preferences -> Java -> Installed JREs -> Execution Environments -> JavaSE-21 on the left and JRE [21.0.8] [perfect match]
   -> Apply and Close
2. Preferences -> Java -> Installed JREs -> Select JRE [21.0.8] (default) -> Apply -> Apply and Close
3. Package Explorer -> right-click the project directory -> Build Path -> Java Build Path -> Libraries -> delete the old JRE
   -> Add Library -> JRE System Library -> Workspace default JRE (JRE [21.0.8]) -> Finish
4. Package Explorer -> right-click the project directory -> Build Path -> Java Compiler -> Choose a drop down option
   of "Compiler compliance level" to 21 -> Apply -> Apply and Close
5. Package Explorer -> right-click the project directory -> Properties -> Resource ->
   Text file encoding -> select Other: -> choose UTF-8 from the dropdown menu -> Apply and Close

## Linking GitHub to a project
### git CLI
1. Create a GitHub remote repo.
2. In the local repo terminal, use git CLI to add the remote repo as local's origin:
```
git remote add origin http://github.com/...
```
Then, use this command to auto-reconcile divergent branches when doing `git pull`
```
git config --global pull.rebase true
```

### Built-in GUI
1. Package Explorer -> right-click the project directory -> Team -> Share Project -> check
Use or create repository in parent folder of project -> select . folder under the project's directory
-> Finish
2. Window -> Show View -> Other -> Git -> Git Staging