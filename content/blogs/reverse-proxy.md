+++
date = '2020-05-30T23:18:55+05:30'
draft = false
title = 'Reverse Proxy'
+++

Let’s first talk about what’s a proxy. A proxy is a server that accepts connections from clients, which actively configured the proxy server on their machines, in their network settings.

When a client makes a connection to a server, the requests always pass through that proxy server.

This practice has several uses. Companies and organizations can set up proxy servers to filter connections, provide more security, and log traffic. Without using the proxy, clients can’t reach the outside network. Proxy servers are also useful to provide privacy.

A reverse proxy on the other hand is set up by the server. It’s completely transparent to clients, they don’t know this middleman exists, but it does a very useful job on the servers, filtering requests and sending them to the appropriate service that handles them.

It’s common to use Nginx as a reverse proxy, and have services listening on internal ports, unaccessible from the outside. 

Nginx in this case serves as the main request handler, and sends the appropriate requests, for example linking special subfolders or URLs to specific services.

We can have 2 or more different Python apps doing different things, and the user does not need to know about that. 

Reverse proxies are typically implemented to help increase security, performance, and reliability.

Beside this routing functionality, which is what us developers will mostly use it for, reverse proxies are also great to filter and protect from attacks serving as a firewall, to introduce caching, to configure SSL, to handle load balancing, to set rate limiting, and much more. 
