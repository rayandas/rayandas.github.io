+++
date = '2020-09-22T20:48:37+05:30'
draft = false
title = 'Status Codes'
+++

Every HTTP response has a status code. There are around 60+ status codes but these are the most common in real life:

### 2×× Success

200 OK
The request has succeeded

### 3xx's aren't errors, just redirect to somewhere else.

301 Moved Permanently
The target resource has been assigned a new permanent URI and any future references to this resource ought to use one of the enclosed URIs.

302 Found (temporary redirection)
The target resource resides temporarily under a different URI. Since the redirection might be altered on occasion, the client ought to continue to use the effective request URI for future requests.

304 Not Modified
A conditional GET or HEAD request has been received and would have resulted in a 200 OK response if it were not for the fact that the condition evaluated to false.

4xx Client error (it made somekind of invalid request)

400 Bad Request
The server cannot or will not process the request due to something that is perceived to be a client error (e.g., malformed request syntax, invalid request message framing, or deceptive request routing).

403 Forbidden (API key/OAuth/something needed)
The server understood the request but refuses to authorize it.

404 Not Found (we all know this one)
The origin server did not find a current representation for the target resource or is not willing to disclose that one exists.

429 Too Many Requests (you are being rate limited)
The user has sent too many requests in a given amount of time ("rate limiting").

5xx Something is wrong with the server

500 Internal Server Error
The server encountered an unexpected condition that prevented it from fulfilling the request.

503 Service Unavailable (could mean proxy(nginx) couldn't connect to the server)
The server is currently unable to handle the request due to a temporary overload or scheduled maintenance, which will likely be alleviated after some delay.

504 Gateway Timeout (server was too slow to respond)
The server, while acting as a gateway or proxy, did not receive a timely response from an upstream server it needed to access in order to complete the request.

