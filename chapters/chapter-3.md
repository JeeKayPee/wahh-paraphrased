# Web Application Technologies

## The HTTP Protocol

Hypertext transfer protocol (HTTP) - core communications protocol to access the World Wide Web

Message based protocol - client and server exchange request and response messages, respectively.

Connectionless protocol - each message exchange is an autonomous transaction and may use a different TCP connection, even though TCP is stateful transport mechanism.


### HTTP Requests

```http
GET /user/123/profile HTTP/1.1
Accept-Language: en-us
Accept: text/html
Referer: https://example.com/user/123/profile
User-Agent: Mozilla/4.0 (compatible; MSIE5.01; Windows NT)
Host: www.example.com
Connection: Keep-Alive
Cookie: SessionId=5B3234GD35125J618951V12513
```

The first line of every HTTP request consists of three items, seperated by spaces:

1. A verb indicating the HTTP Method
2. The requested URL with optional parameters
3. The HTTP Version being used

Some of the headers in a request message

* Referer - the URL from which the request originated.
* User-Agent - information about the browser
* Host - the hostname that appears in the full URL
* Cookie - submits additional parameters issued by the server to the client


### HTTP Responses

```http
HTTP/1.1 200 OK
Server: Microsoft-IIS/6.0
X-Powered-By: ASP.NET
Set-Cookie: tracking=tI31Fs342vFSfs
Date: Tue, 19 May 2020 08:23:14 GMT
Cache-Control: no-cache
Pragma: no-cache
Expires: Thu, 01 Jan 1970 00:00:00 GMT
Content-Length: 88
Content-Type: text/html
Connection: Closed

<html>
<body>
<h1>Hello, Martin</h1>
</body>
</html>
```

The first line of every HTTP response consists of three items, seperated by spaces:

1. The HTTP Version being used
2. Status code indicating the result of the request
3. A textueal "reason phrase" further describing the status of the response.


Some of the headers in a request message:

* Server - the web sever software
* Set-Cookie - issues a cookie to the browser
* Pragma - instructs the browser whether to store the response in its cache
* Expires - when the response expires and should it be cached
* Content-Type - the type of content inside the response message body
* Content-Length - the length of the content inside the response message body in bytes


### HTTP Methods

* GET - This method is designed to retrieve resources. It can send parameters to the resource using the URL query string. Since URLs are displayed on-screen and logged in various places, such as browser history and web server's access logs, and also trasmitted to the Referer header, the query string should not contain any sensitive information.

* POST - This method is designed to perform actions. Request parameters can be sent both in the URL query string and in the body of the request message. Any parameters sent in the body will not be logged, which makes it a secure way of transmitting sensitive information. The browser does not automatically reissue a POST request and always wanrs the user in such a case. This ensures that an action is only performed once.

* HEAD - Functions the same way as a GET request, except that the server should not return a message body. However, the response headers remain the same. This can be used to check if a resource is available before retrieving it.

* TRACE - Designed to return the exact contents of the request message. This is used to detect the effect of a possible proxy manipulating the request between the client and the server.

* OPTIONS - sks the server to report all HTTP methods available for a particular resource. The server typically returns a response containing an **Allow** header that lists these methods.

* PUT - Attempts to upload the specified resource to the server, using the contents contained in the body of the request. This could be leveraged to an arbitrary file upload.


### URLS

A uniform resource locator is a unique identifier for a web resource throught which it can be retrieved with. 
The format for most URLs is as follows:

```
protocol://hostname[:port]/[path/]file[?param=value]
```

This is also referred as an absolute form. Relative forms could be used as a way of navigation within the web application.

The port is needed only if it differs from the default one (80).

> URI - **uniform resource identifier** may be used instead of URL, but it is really only used in formal specifications and by those who want to exhibit their pedantry.


### REST

**REpresentational State Transfer** is a style of architecture for distributed systems in which requests and responses contain representations of the current state of the system's resources. The core technologies employed in the World Wide Web, including the HTTP protocol and the format of URLs, conform to the REST architectural style.

Although URLs containing parameters within the query string do themselves conform REST constraints, the term "REST-style URL" is often used to signify a URL that contains its parameters within the URL file path, rather than the query string. For example the following URL containing a query string

```
http://example.com/search?animal=dog&breed=pug
```

corresponds to the following URL containing "REST-style" parameters:

```
http://example.com/search/dog/pug
```

### HTTP Headers

#### General headers

* Connection - Tells the other side of communication wheter to keep or close the connection for further messages
* Content-Type - the type of content inside the message body
* Content-Length - the length of the content inside the message body in bytes
* Content-Encoding - the kind of encoding used inside the message body
* Transfer-Encoding - specifies chunked encoding transmitted over HTTP


#### Request Headers

* Accept - what kind of content the client is willing to accept
* Accept-Encoding - what kind of content encoding the client is willing to accept
* Authorization - submits credentials to the server for build-in HTTP authentication types
* Cookie - submits additional parameters issued by the server to the client
* Host - the hostname that appears in the full URL
* If-Modified-Since - the last recieved copy of a resource.
* If-None-Match - an entity tag, denoting the resource submitted to the server
* Origin - domain name in cross-domain Ajax requests
* Referer - URL from which the request originated.
* User-Agent - information about the browser


#### Response Headers

* Access-Control-Allow-Origin - can the resource be retrieved via cross-domain Ajax request
* Cache-Control - passes caching directives to the browser
* ETag - an identifier denoting the contents of the message body which help the browser decide whether to use instead of a cached copy
* Expires - when the response expires and should it be cached
* Location - the target in redirection responses
* Pragma - should the browser store the response in its cache
* Server - the web sever software
* Set-Cookie - issues a cookie to the browser for further requests
* WWW-Authenticate - authentication details for 401 status codes messages
* X-Frame-Options - should the current response be loaded within a frame and how


## Cookies

The cookie mechanism enables the server to send items of data to the client, which will continue to be resubmitted in each subsequent request, without any action by the user.

A server issues a cookie using the **Set-Cookie** header and the browser automatically adds the following header to sebsequent requests back to the server. Cookies are submitted using a key-value pair and multiple cookies could be sent by the server using a semicolon separating them from each other.

Cookies also have optional attributes that could be set by the server:

* expires - sets a date till the cookie is valid and is stored in the persistent browser session. If missing, the cookit is used only in the current browser session
* domain - specifies the domain in which the cookie is valid. This must be the same or a parent domain of which the cookie was received
* path - specifies the path in which the cookie is valid
* secure - the cookie would only be submitted in HTTPS requests
* HttpOnly - the cookie cannot be directly accessed via client-side JavaScript


## Status Codes

Each HTTP response must contain a status code in the first line, indicating the result of the request. The status codes fall into five groups, according to the code's first digit:

* 1xx - Informational
* 2xx - Successful
* 3xx - Redirect
* 4xx - Client error
* 5xx - Server error


## HTTPS

HTTP uses plain TCP which is unencrypted and could be vulnerable to network poisoning.
HTTP(S), the "S" stanting for secure, is essentially the same application layer protocol but tunneled over the Secure Sockets Layer (SSL) transport mechanism. This protects privacy and integrity and does not change the way HTTP message functions work.

> SSL has strictly been superseded by transport layer security (TLS), but the latter usually still is referred to using the older name.


## HTTP Proxies

A server that mediates access between the client and the web server. A configured browser will send all requests to the targeted proxy, which will relay the request to the relevant server and forward back the response. Most proxies provide additional services - caching, authentication and access control.

> When a browser issues an unencrypted HTTP request to a proxy server, it places the full URL into the request including the prefix `http://`, the server's hostname and optionally a port number

> When HTTPS is being used, the browser cannot perform the SSL handshake with the proxy server, because this would break the secure tunnel and leave communications vulnerable to interception attacks. Hence the proxy could only act as a TCP-level relay to the destination server.


## HTTP Authentication

HTTP protocol includes its own authentication mechanisms using various schemes:

* Basic - sends credentials as a base64 encoded string in a request header with each message
* NTLM - a challenge response mechanism and uses a version of Windows NTLM protocol
* Digest - a challenge response mechanism and uses MD5 checksums of a nonce with the user's credentials

These mechanisms are rare in Internet deployed web application. They are more common within orgranisations to access intranet-based services.

> A common myth is that basic authentication is insecure due to the way it transmits user credentials. It is no worse than all other web application authentication mechanisms and secure enough when HTTPS is being used to encrypt the HTTP message


# Server Side Functionality

## The Java Platform

* Enterprise Java Bean (EJB) - Heavyweight software component encapsulating the logic of a specific business function within the application. EJBs are intended to take care of various technical challenges such as transaction integrity
* Plain Old Java Object (POJO) - An ordinary java object. Used to denote user defined objects
* Java Servlet - Object that resides on the application server. It recieves HTTP requests and returns HTTP responses
* Java Web Container - Platform or engine that provies runtime enviroment for Java-based web applications. Examples of JWC are Apache Tomcat, BEA, WebLogic and JBoss

## ASP.NET

- Microsoft’s web application framework
- Uses Microsoft’s .NET Framework, which provides a virtual machine
(the Common Language Runtime) and a set of powerful APIs
- Applications can be written in any .NET language, such as C# or VB.NET
- Helps protect against common web vulnerabilities such as cross-site scripting, without requiring any effort from the developer
- ASP.NET applications are actually created by beginners who lack any awareness of the core security problems faced by web applications

## PHP

- LAMP stack (Linux, Apache, MySQL and PHP)
- The design and default configuration of the PHP framework has historically made it easy for programmers to unwittingly introduce security bugs into their code
- Several defects have existed within the PHP platform itself that often could be exploited via applications running on it

## Ruby on Rails

- Strong emphasis on Model-View-Controller architecture
- Breakneck speed in creating fully fledged data-driven applications
- Several vulnerabilities, including the ability to bypass a “safe mode,” analogous to that found in PHP
- [More details on recent vulnerabilities](www.ruby-lang.org/en/security/) 

## SQL

- Structured Query Language
- Used to access data in relational databases - Oracle, MS-SQL server and MySQL
- Nearly all application functions involve interaction with backend data stores
- Web applications may incorporate user-supplied input into SQL queries that are executed by the back-end database.
- Attackers may be able to submit malicious input to interfere with the database and potentially read and write sensitive data.

## XML

- Extensible Markup Language
- Specification for encoding data in a machine-readable form
- Separates a document into content (data) and markup (which annotates the data)
- Markup is primarily represented using tags
- Tags may include attributes (name-value pairs)
- Documents often include a Document Type Definition (DTD)
- Used extensively in web applications (both server and client side)

## Web Services

- Web services use Simple Object Access Protocol (SOAP) to exchange data
- SOAP typically uses the HTTP protocol to transmit messages and represents
data using the XML format
- You are most likely to encounter SOAP being used by the server-side application to communicate with various back-end systems
- If user-supplied data is incorporated directly into back-end SOAP messages, similar vulnerabilities can arise as for SQL
- If a web application also exposes web services directly, these are also worthy of examination
- The server normally publishes the available services and parameters using the Web Services Description Language (WSDL) format
- Tools such as soapUI can be used to create sample requests based on a published WSDL fi le to call the authentication web service, gain an authentication token, and make any subsequent web service requests
- A typical SOAP request is as follows

```http
POST /doTransfer.asp HTTP/1.0
Host: mdsec-mgr.int.mdsec.net
Content-Type: application/soap+xml; charset=utf-8
Content-Length: 891
<?xml version=”1.0”?>
<soap:Envelope xmlns:soap=”http://www.w3.org/2001/12/soap-envelope”>
<soap:Body>
<pre:Add xmlns:pre=http://target/lists soap:encodingStyle=
“http://www.w3.org/2001/12/soap-encoding”>
<Account>
<FromAccount>18281008</FromAccount>
<Amount>1430</Amount>
<ClearedFunds>False</ClearedFunds>
<ToAccount>08447656</ToAccount>
</Account>
</pre:Add>
</soap:Body>
</soap:Envelope>
```

# Client Side Functionality

## HTML

- Hypertext Markup Language is a tag-based language
- Describes the structure of documents that are rendered within the browser
- Has developed into a rich and powerful language
- XHTML is a development of HTML that is based on XML
- XHTML has a stricter specification than older versions of HTML
- XHTML's motivations is to avoid various compromises and security issues


# Other Resources
* *HTTP: The Definitive Guide* by David Gourley
* *World Wide Web Consortium* at [www.w3.org](https://www.w3.org)