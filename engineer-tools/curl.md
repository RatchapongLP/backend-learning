# `curl` fundamentals

### Funtionality
- Used for transferring data from or to a server.
- Supports FTP, FTPS, HTTP, HTTPS, IMAP, LDAP, SFTP, SMTP, TELNET.
- If the protocol is not specified, it will try to match one, by default with http.
    ```
    curl google.com --> curl http://google.com
    curl ftp.xxx --> curl ftp://ftp.xxx
    ```
- Pagination is supported.
    ```
    curl "http://example.com/archive[1996-1999]/vol[1-4]/part{a,b,c}.html"
    ```

### Options

- `curl -i <url>` displays headers in addition to the response body.
- `curl -I <url>` displays only headers without the response body.

- `curl -o <file name> <url>` or `curl --output <file name> <url>` saves the response 
into the `<file name>` file.
    ```
    % curl --output jdk-21.tar.gz --location https://download.oracle.com/java/21/latest/jdk-21_macos-aarch64_bin.tar.gz
    % ls
    jdk-21.tar.gz
    ```

- `curl -O <url>` also saves the response but to the file with the name of the remote file.  
    ```
    % curl -O https://download.oracle.com/java/21/latest/jdk-21_macos-aarch64_bin.tar.gz
    % ls
    jdk-21_macos-aarch64_bin.tar.gz
    ```

- `curl -L <url>` or `curl --location <url>` auto-redirects the request to the destination as required by the server.
    ```
    % curl google.com
    <HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
    <TITLE>301 Moved</TITLE></HEAD><BODY>
    <H1>301 Moved</H1>
    The document has moved
    <A HREF="http://www.google.com/">here</A>.
    </BODY></HTML>
    
    % curl -L google.com
    <!doctype html><html itemscope="" itemtype="http://schema.org/WebPage" lang="th"><head>
    <meta content="text/html; charset=UTF-8" http-equiv="Content-Type"><meta content=
    "/images/branding/googleg/1x/googleg_standard_color_128dp.png" itemprop="image">
    <title>Google</title><script nonce="KHtt5qGSP_ISmcTHtEL7eA"> 
    ...
    ```

  - `curl -d '<body>' <url>` or `curl --data '<body>' <url>` sends the body message with the request.  
    - Set the default method as POST.
    - Automatically sets the header `Content-Type: application/x-www-form-urlencoded` 
    - It does not encode the `<body>` unless using `curl --data-urlencode '<body>' <url>` 
    (`curl -d-urlencode` is not a valid form).
    - If the `<body>` is already encoded, `-d` should be used, e.g. 
    ```
    curl -d "name=John+Doe&city=Bangkok" <url>
    ``` 
    If the `<body>` is *not* encoded, `--data-urlencoded` should be used and the key-value pairs
    should be separated, e.g.
    ```
    curl --data-urlencode "name=John Doe" \
        --data-urlencode "city=Bangkok" \
        <url>
    ```
    - `'` and `"` can be used to enclose the `<body>` with some difference. 
    `'` makes the `body` as literals. `"` makes `body` as parameterized string.
    ```
    curl -d '{"name": "John Doe", "city": "Bangkok"}' <url>
    
    city="Bangkok"
    curl -d "{\"name\": \"John Doe\", \"city\": \"$city\"}" <url>
    ```

- `curl -X <http method>`
- `curl -u <username>:<password> `

