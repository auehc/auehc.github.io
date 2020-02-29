## Web Application Exploitation
I will start this by defining software exploitation.
> Software exploitation is the process, usually defined in code, that can
> manipulate flaws in a piece of sofware; causing it to act in ways
> unintended by the original author.
This may lead you to ask how this has anything to do with the web and
websites. Well, when exploiting the web, we are looking at the technologies
that build and host the website to find vulnerabilities that could lead to
us causing the server to execute unintended commands.

## How things on the web are located
Web resources are identified via Uniform Resource Locators (URL). Each well
formed URL is meant conclusively address and uniquely identify a single
resource on a remote server. Psuedo-URLs use a similar syntax to provide
convenient access to browser-level features, at times psuedo-URL actions
can have a significant impact on the security of a site that links to them.
* [URL syntax RFC](https://tools.ietf/org/html/rfc3986)
* Practical uses [1](https://tools.ietf/org/html/rfc1738) [2](https://tools.ietf/org/html/rfc2616)

## The language of the web
Web servers usually communicate using Hyper-Text Transfer Protocol (HTTP).
The secured version of HTTP is called HTTPS. HTTP servers are typically
bound to port 80 and HTTPS port 443. [1](https://tools.ietf.org/html/rfc3986) [2](https://tools.ietf/org/html/rfc6265)
There are six methods that web clients use to communicate with web servers,
* GET
* POST
* HEAD
* PUT
* TRACE
* OPTIONS
Each method has its own unique purpose that tells the server what actions it
needs to perform. When a server receives a HTTP request, it will process it,
and respond with a code and content. These codes can fall in one of four different
classes.
* 200 - 299: success
* 300 - 399: redirection
* 400 - 499: client side error
* 500 - 599: server side error

## Web Hacking Tools
There are a plethora of tools that can assist in the process of web exploitation.
One of the most popular of these tools is BurpSuite, which is a web proxy. This
tools is able to intercept web requests for analysis, modification, and attack.