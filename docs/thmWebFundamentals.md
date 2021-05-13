# Web Fundamentals

## HTTP requests/responses

* Finding the Server

    - DNS request is made; URL turned into IP

    - IP Addresses -- 4 groups of numbers, each 0-255, called an *octet*

* HTTP GET request

    - browser asking IP address for web page

    - GET is an example of a HTTP verb

    - extra resources, like JavaScript, images, or CSS files retreived in seperate GET requests


## Web Servers

* **Web Server** -- software that receives and responds to HTTP(S) requests

    - Examples:

        + Apache

        + Nginx

        + Microsoft's IIS

* HTTP runs on port 80 by default

* HTTPS runs on port 443 by default

* Actual Web Page Contents:

    - HTML -- defines structure/content of page

    - CSS -- changes how the page looks; makes it 'fancy'

    - JavaScript -- makes pages interactive and loads extra content


## More HTTP Verbs and request formats

* 9 different HTTP 'verbs' aka methods

* **POST** requests 

    - used to send data to web server

    - like adding a comment or performing a login

    - most important info is in header -- OS & browser

* Server Responses:

    - 100-199: Information

    - 200-299: Successes -- 200 OK is the 'normal' response for a GET

    - 300-399: Redirects -- the info you want is elsewhere

    - 400-499: Client errors -- like 404:Not Found

    - 500-599: Server erros -- something wrong server side

    - [Link to more info on status codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)


## Cookies

* **Cookies**

    - small bits of data stored in your browser

    - each browser stores cookies separately

    - sent with every HTTP request made to a server

    - most common uses: 

        + for session management

        + advertising -- tracking cookies


* Why Cookies?

    - HTTP is *stateless* -- each request is independent, no state is tracked internally

    - keep track of:

        - whats in your shopping cart
        
        - who you are

        - what you've done on the website

* Parts of a Cookie

    - **Name** -- identifies cookie

    - **Value** -- where data is stored

    - **Expiry Date** -- when browser will get rid of cookie automatically

    - **Path** -- what code request is sent with

* Using cookies

    - logging on to a website gives you a *Session Token*, for that website

    - lets web servers differentiate your requests from someone else

    - stealing someone else's session token means you can impersonate them

* Manipulating cookies

    - Dev tools in a browser

    - curl command

* [Cookies Info page from Mozilla](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies)


## cURL

* **cURL** -- making HTTP requests without a browser
```
curl https://tryhackme.com
```

* specify request type -X POST
```
curl -X POST https://tryhackme.com
```


## Mini CTF

* Target IP: 10.10.207.208 

* Web Server address -- "http://10.10.207.208:8081"


1. GET request to /ctf/get
```
curl http://10.10.207.208:8081/ctf/get

thm{162520bec925bd7979e9ae65a725f99f}
```

2. POST request with body "flag_please" to /ctf/post
```
curl -X POST --data flag_please http://10.10.207.208:8081/ctf/post

thm{3517c902e22def9c6e09b99a9040ba09}
```

3. GET request to /ctf/getcookie, saving to "cookies" for readability
```
curl -G -c cookies http://10.10.207.208:8081/ctf/getcookie
cat cookies

thm{91b1ac2606f36b935f465558213d7ebd}
```

4. sending cookie with Name=flagpls, Value=flagpls to /ctf/sendcookie
```
curl -b flagpls=flagpls http://10.10.207.208:8081/ctf/sendcookie

thm{c10b5cb7546f359d19c747db2d0f47b3}

```


---
[back to TryHackMe main page](thm.md)

[back to Index/Table of Contents](index.md)
