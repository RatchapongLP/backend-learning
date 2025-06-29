# JDK setup steps

## For macOS, m-series chips
### Manual method for individual user setup (a bit unconventional for macOS)
1. Download jdk tar.gz from a reliable source. In this tutorial, the link from ORACLE website is used - 
`https://download.oracle.com/java/21/latest/jdk-21_macos-aarch64_bin.tar.gz`. You can follow the link to download or use CLI as:
```
% cd ~/opt
% curl --output jdk-21.tar.gz --location https://download.oracle.com/java/21/latest/jdk-21_macos-aarch64_bin.tar.gz
```
Other jdk versions - 8, 11, 24, etc. - and jdk sources - corretto, etc. - can be used as well.
2. Extract the `jdk-21.tar.gz` using this command:
```
% tar -xvzf jdk-21.tar.gz
```
The folder should look like this:
```
~/opt
└── jdk-21.0.7.jdk
    └── Contents
        ├── CodeResources
        ├── Home
        │   ├── LICENSE -> legal/java.base/LICENSE
        │   ├── README
        │   ├── bin
        │   │   ├── jar
        │   │   ├── jarsigner
        │   │   ├── java
        │   │   ├── javac
        │   │   ├── javadoc
        │   │   └── ...
        │   │     
        │   ├── conf
        │   ├── include
        │   ├── ...
        │   └── release
        ├── Info.plist
        ├── MacOS
        └── _CodeSignature
```

3. Set the environment variables permanently for all new shell sessions started.
```
% nano ~/.zshrc

// Type into the config file
export JAVA_HOME="$HOME/opt/jdk-21.0.7/Contents/Home"
export PATH="$JAVA_HOME/bin:$PATH"

// Save the file and exit
[Ctrl] + [O]
[Return]
[Ctrl] + [X]
```

4. Start a new shell (`cmd + N`) and check:
```
% echo $JAVA_HOME
/Users/<username>/opt/jdk-21.0.7/Contents/Home

% echo $PATH
/Users/<username>/opt/jdk-21.0.7/Contents/Home/bin:/opt/homebrew/bin:/opt/homebrew/sbin:/usr/local/bin:/System/Cryptexes/App/usr/bin:/usr/bin:/bin:/usr/sbin:/sbin:/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/local/bin:/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/bin:/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/appleinternal/bin

% which java
/Users/<username>/opt/jdk-21.0.7/Contents/Home/bin/java

% java --version
java 21.0.7 2025-04-15 LTS
Java(TM) SE Runtime Environment (build 21.0.7+8-LTS-245)
Java HotSpot(TM) 64-Bit Server VM (build 21.0.7+8-LTS-245, mixed mode, sharing)
```