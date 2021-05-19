# HTTP in Detail

* **HTTP** -- HyperText Transfer Protocol

    - used whenever you view a website

    - developed by Tim Berners-Lee & Team between 1989-1991

    - the set of rules for communicating with web servers for transmitting:

        + HTML

        + Images

        + Videos

        + etc..

* **HTTPS** -- HyperText Transfer Protocol Secure

    - the secure version of HTTP

    - data is encrypted in HTTPS

    - encryption to:

        + stop other people from seeing your data

        + make sure you're *talking* to the correct web server, not an imposter


## Requests and Responses

* **URL** -- Uniform Resource Locater

    - Scheme 

        + instructs on what protocol to use for accessing resources: HTTP, HTTPS, FTP

    - User 

        + some services require authentication to login, you can put credentials in the URL

    - Host

        + The domain name or IP address of the server you're attempting to connect to

    - Port
    
        + the port you're going to connect to, usually 80 for HTTP and 443 for HTTPS

    - Path

        + the file name or location of the recource you're trying to access

    - Query String

        + extra bits of information that can be sent to the requested path

        + ie: /blog?id=1 -- tells blog path you want the article with id of 1

    - Fragment

        + a reference to a location on the actual page requested

        + commonly used for pages with long content, and links to specific parts to it


## HTTP Methods

* GET Request

    - getting info from server

    - ie: reading an article

* POST Request
    
    - submitting data to the webserver/creating new records

    - ie: creating a new user account

* PUT Request

    - used to submit data to webserver to update information

    - ie: updating an email address

* DELETE Request

    - deleting information/records from a webserver


## HTTP Status Codes

* 100-199 -- Information Response
* 200-299 -- Success
* 300-399 -- Redirection
* 400-499 -- Client Errors
* 500-599 -- Server Errors

* Common Status Codes:

    - 200 -- OK
    - 201 -- Created; a resource has been created
    - 301 -- Permanent Redirect
    - 302 -- Temporary Redirect
    - 401 -- Not Authorised
    - 403 -- Forbidden
    - 405 -- Method Not Allowed
    - 500 -- Internal Service Error
    - 503 -- Service Unavailable


## Headers

* additional bits of data you can send to the web server when making requests

* Common **Request** Headers
    
    - **Host**
        + some web servers have multiple websites

        + by providing *Host* headers, you can tell it which one you need

        + otherwise you get default website

    - **User-Agent**
        + browser software and version number

        + helps format website properly

    - **Content-Length**
        + tells the web server how much data to expect with the web request

        + ensures no data is missing

    - **Accept-Encoding**
        + tells web server what types of compression methods the browser supports

        + this means data can be made smaller for transmitting over the internet

    - **Cookie**
        + data sent to the server to remember your information

* Common **Response** Headers

    - **Set-Cookie**
        + information to store which gets sent back to web server on each request

    - **Cache-Control**
        + how long to store the content of the response in the browser's cache before requesting again

    - **Content-Type** 
        + tells client what type of data is being returned

        + ie: HTML, CSS, JavaScript, Images, PDF, Video, etc

        + so the browser knows how to process the data


## Cookies

* Cookies are saved when receiving a *Set-Cookie* header from a web server

* Every further request you make, you send the cookie data back to the web server

* Most commonly used for website authentication

* Cookies can be viewed in a browser with the built-in *Developer Tools*


## Making Requests - Practical with in-browser Browser

Making a GET request to /room
```
THM{YOU'RE_IN_THE_ROOM}
```

Make a GET request to /blog and using the gear icon set the id parameter to 1 in the URL field
```
THM{YOU_FOUND_THE_BLOG}
```

Make a DELETE request to /user/1
```
THM{USER_IS_DELETED}
```

Make a PUT request to /user/2 with the username parameter set to admin
```
THM{USER_HAS_UPDATED}
```

POST the username of thm and a password of letmein to /login
```
THM{HTTP_REQUEST_MASTER}
```

---
[back to TryHackMe main page](index.md)

[back to Index/Table of Contents](index.md)
