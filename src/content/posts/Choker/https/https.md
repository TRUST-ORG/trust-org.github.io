---
title: HTTP in Detail
published: 2025-09-01
author: 'Choker'
description: Explanation of HTTP, its structure, methods, status codes, headers, cookies, and exercises
image: 'https://tryhackme-images.s3.amazonaws.com/room-icons/66704dd0e54a1f39bff7b1a1-1735573858833'
tags: ["HTTP", "Web"]
category: 'Choker'
draft: false
---


## Definition of HTTP(S)

HTTP (HyperText Transfer Protocol) is the protocol used for communication between web browsers (clients) and web servers.  
It allows transferring web resources such as HTML, images, videos, and other content.

HTTPS (HTTP Secure) is the encrypted version of HTTP, adding security and authentication.  
It ensures:
- Data confidentiality (encryption)  
- Server identity verification  

If HTTPS certificate validation fails, browsers will show a warning.  
Example flag in exercises: THM{INVALID_HTTP_CERT}.

---

## Requests and Responses

### URL Components
A URL (Uniform Resource Locator) has the following parts:
- Scheme: http, https
- User: Optional (for authentication)
- Host: Domain name or IP address
- Port: Default 80 (HTTP), 443 (HTTPS), range 1–65535
- Path: Resource location on the server
- Query string: Example ?id=1
- Fragment: Example #section

### Example HTTP Request
GET / HTTP/1.1
Host: tryhackme.com
User-Agent: Mozilla/5.0
Referer: https://tryhackme.com/

### Example HTTP Response
HTTP/1.1 200 OK
Server: nginx/1.15.8
Date: Fri, 09 Apr 2021 13:34:03 GMT
Content-Type: text/html
Content-Length: 98

<html>…</html>

- Content-Type: Specifies returned data type  
- Content-Length: Specifies response size  

---

## HTTP Methods

- GET → Retrieve information  
- POST → Submit data / create resource  
- PUT → Update existing resource  
- DELETE → Remove resource  

---

## HTTP Status Codes

### Categories
- 1xx → Informational  
- 2xx → Success  
- 3xx → Redirection  
- 4xx → Client-side errors  
- 5xx → Server-side errors  

### Common Codes
- 200 OK, 201 Created  
- 301 Moved Permanently, 302 Found  
- 400 Bad Request, 401 Unauthorized, 403 Forbidden, 404 Not Found, 405 Method Not Allowed  
- 500 Internal Server Error, 503 Service Unavailable  

---

## HTTP Headers

### Request Headers (Client → Server)
- Host  
- User-Agent  
- Content-Length  
- Accept-Encoding  
- Cookie  

### Response Headers (Server → Client)
- Set-Cookie  
- Cache-Control  
- Content-Type  
- Content-Encoding  

---

## Cookies

Cookies are small pieces of data stored on the client, used for:
- Authentication  
- Session management  
- Tracking preferences  

Servers set cookies using the Set-Cookie header, and clients automatically send them in future requests.

---

## Hands-on Exercises & Flags

- GET /room → THM{YOU’RE_IN_THE_ROOM}  
- GET /blog?id=1 → THM{YOU_FOUND_THE_BLOG}  
- DELETE /user/1 → THM{USER_IS_DELETED}  
- PUT /user/2 (username=admin) → THM{USER_HAS_UPDATED}  
- POST /login (username=thm, password=letmein) → THM{HTTP_REQUEST_MASTER}  

---

## Summary Table

| Section         | Key Learnings                                        |
|-----------------|------------------------------------------------------|
| 1. HTTP(S)      | Difference between HTTP and HTTPS, certificate check |
| 2. Req/Resp     | URL structure, request/response format               |
| 3. Methods      | GET, POST, PUT, DELETE usage                         |
| 4. Status Codes | Categories and examples                              |
| 5. Headers      | Common request and response headers                  |
| 6. Cookies      | Session persistence and authentication               |
| 7. Exercises    | Practice flags with different HTTP methods           |

---

## Finishing

Now you should understand:
- How HTTP(S) works  
- The structure of requests and responses  
- The purpose of methods, status codes, headers, and cookies  
- How to practice with real exercises  

You can also test manually with tools like cURL:

curl -I https://tryhackme.com

Or with telnet:

telnet tryhackme.com 80
GET / HTTP/1.1
Host: tryhackme.com

These commands allow you to directly view headers and responses in practice.

