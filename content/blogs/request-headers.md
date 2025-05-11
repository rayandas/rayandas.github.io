+++
date = '2020-09-21T16:01:00+05:30'
draft = false
title = 'The Most Important HTTP Request Headers'
+++

When a browser requests a resource from a server, it uses HTTP. This request includes a set of key-value pairs giving informations like the version of the browser or what file format it understands. There key-value pairs are called request headers. 

The server answers with the requested resource but also sends response headers giving information on the resource or the server itself.

Below are the most important request headers:

1. Host: The domain. The only required header.
```bash
Host: website-name.com
```

2. User-Agent: Name + version of your browser and OS.
```bash
User-Agent: curl/7.64.1
```

3. Referer: Website that linked or included the resource.
```bash
Referer: https://website-name.com
```

4. Authorization: A password or API token
```bash
Authorization: Basic xyz(base64 encoded user: password)
```

5. Cookie: Send cookies the server sent earlier and keeps you logged in.
```bash
Cookie: user=john
```

6. Range: Let's you continue downloads ("get bytes 100-200")
```bash
Range: bytes=100-200
```

7. Cache-Control: "max-age=60" means cached responses must be less than 60 seconds old.

8. If-Modified-since: Only send if resource was modified after this time.
```bash
If-Modified-Since: Sun, 21 Sep...
```

9. If-None-Match: Only sent if the ETag doesn't match those listed.
```bash
If-None-Match: "z9843ca"
```

10. Accept: MIME type you want the response to be. 
```bash 
Accept: image/png
```

11. Accept-Encoding: Set this to "gzip" and you'll probably get a compressed response.
```bash
Accept-Encoding: gzip
```

12. Accept-Language: Set this to "fr-CA" and you might get a response in French.
```bash
Accept-Language: fr-CA
```

13. Content-Type: MIME type of request body, e.g. "application/json"

14. Content-Encoding: Will be "gzip" if the request body is gzipped.

15. Connection: "close" of "keep-alive" Whether to keep the TCP connection open.

