# Maven setup steps

## For macOS
1. Download maven bin.tar.gz from the apache maven official site  
`https://dlcdn.apache.org/maven/maven-3/3.9.10/binaries/apache-maven-3.9.10-bin.tar.gz`.  
You can follow the link, or download using CLI as:
```
% cd ~/opt
% curl -O https://dlcdn.apache.org/maven/maven-3/3.9.10/binaries/apache-maven-3.9.10-bin.tar.gz
```

2. Extract the `apache-maven-3.9.10-bin.tar.gz` using this command:
```
% tar -xvf apache-maven-3.9.10-bin.tar.gz
```
***Note***: *the `-z` option (tells tar to use gzip compression/decompression) is omitted but
the archive file was extracted successfully in the end.*  <p>
The folder should look like this:
```
~/opt
└── apache-maven-3.9.10
    ├── LICENSE
    ├── NOTICE
    ├── README.txt
    ├── bin
    │   ├── m2.conf
    │   ├── mvn
    │   ├── mvn.cmd
    │   └── ...
    ├── boot/
    ├── conf/
    └── lib/
```

3. Set the environment variables permanently for all new shell sessions started.
```
% nano ~/.zshrc

// Modify the config file after jdk_setup.md tutorial
export JAVA_HOME="$HOME/opt/jdk-21.0.7/Contents/Home"
export MAVEN_HOME="$HOME/opt/apache-maven-3.9.10"
export PATH="$JAVA_HOME/bin:$MAVEN_HOME/bin:$PATH"

// Save the file and exit
[Ctrl] + [O]
[Return]
[Ctrl] + [X]
```

4. Start a new shell (`cmd + N`) and check:
```
% echo $MAVEN_HOME
/Users/<username>/opt/apache-maven-3.9.10

% echo $PATH
/Users/<username>/opt/jdk-21.0.7/Contents/Home/bin:/Users/<username>/opt/apache-maven-3.9.10:/opt/homebrew/bin:/opt/homebrew/sbin:/usr/local/bin:/System/Cryptexes/App/usr/bin:/usr/bin:/bin:/usr/sbin:/sbin:/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/local/bin:/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/bin:/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/appleinternal/bin

% which mvn
/Users/<username>/opt/apache-maven-3.9.10/bin/mvn

% mvn -v
Apache Maven 3.9.10 (5f519b97e944483d878815739f519b2eade0a91d)
Maven home: /Users/<username>/opt/apache-maven-3.9.10
Java version: 21.0.7, vendor: Oracle Corporation, runtime: /Users/<username>/opt/jdk-21.0.7/Contents/Home
Default locale: en_TH, platform encoding: UTF-8
OS name: "mac os x", version: "15.5", arch: "aarch64", family: "mac"
```