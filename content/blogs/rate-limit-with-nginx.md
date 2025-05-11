+++
date = '2020-10-12T17:02:00+05:30'
draft = false
title = 'Rate Limit With Nginx To Protect DoS Attacks'
+++

HTTP DoS protection with Nginx through `ngx_http_limit_conn_module` and `ngx_http_limit_req_module` modules. 

I will show you how to rate limit by user agent (control bots).

The module `ngx_http_limit_conn_module` is used to limit the number of connections per defined key, in particular, the number of connections from a single IP.

Not all connections are counted. A connection is counted only if it has a request processed by the server and the whole request header has already been read.

Example configration:
```bash
http {
    limit_conn_zone $binary_remote_addr zone=addr:10m;

    ...

    server {

        ...

        location /download/ {
            limit_conn addr 1;
        }
```

Directives:
```bash
Syntax: 	limit_conn zone number;
Default: 	—
Context: 	http, server, location
```

Sets the shared memory zone and the maximum allowed number of connections for a given key value. When this limit is exceeded, the server will return the 503 (Service Temporarily Unavailable) error in reply to a request. For example, the directives allow only one connection per IP address at a time:
```bash
limit_conn_zone $binary_remote_addr zone=addr:10m;

server {
    location /download/ {
        limit_conn addr 1;
    }
```

There could be several limit_conn directives. For example, the following configuration will limit the number of connections to the server per client IP and, at the same time, the total number of connections to the virtual server:
```bash
limit_conn_zone $binary_remote_addr zone=one:10m;
limit_conn_zone $server_name zone=two:10m;

server {
    ...
    limit_conn one 10;
    limit_conn two 100;
}
```

The `ngx_http_limit_req_module` module (0.7.21) is used to limit the request processing rate per a defined key, in particular, the processing rate of requests coming from a single IP address. The limitation is done using the `“leaky bucket”` method

Example Configuration:
```bash
http {
    limit_req_zone $binary_remote_addr zone=one:10m rate=1r/s;

    ...

    server {

        ...

        location /search/ {
            limit_req zone=one burst=5;
        }
```

Directives:
```bash
– Syntax: limit_req zone=name [burst=number] [nodelay];
– Default: —
– Context: http, server, location
```

Sets the shared memory zone and the maximum burst size of requests. If the requests rate exceeds the rate configured for a zone, their processing is delayed such that requests are processed at a defined rate. Excessive requests are delayed until their number exceeds the maximum burst size in which case the request is terminated with an error 503 (Service Temporarily Unavailable). By default, the maximum burst size is equal to zero. For example, the directives allow not more than 1 request per second at an average, with bursts not exceeding 5 requests.
```bash
limit_req_zone $binary_remote_addr zone=one:10m rate=1r/s;

server {
    location /search/ {
        limit_req zone=one burst=5;
    }
```

If delaying of excessive requests while requests are being limited is not desired, the parameter nodelay should be used:
```bash
limit_req zone=one burst=5 nodelay;
```

There could be several limit_req directives. For example, the following configuration will limit the processing rate of requests coming from a single IP address and, at the same time, the request processing rate by the virtual server:
```bash
limit_req_zone $binary_remote_addr zone=perip:10m rate=1r/s;
limit_req_zone $server_name zone=perserver:10m rate=10r/s;

server {
    ...
    limit_req zone=perip burst=5 nodelay;
    limit_req zone=perserver burst=10;
}
```

A practical example:

In http section of nginx.conf:
```bash
limit_conn_zone $binary_remote_addr zone=conn_limit_per_ip:20m;
limit_req_zone $binary_remote_addr zone=req_limit_per_ip:20m rate=2r/s;
```
In virtualhost:
```bash
location / {
     limit_req zone=req_limit_per_ip burst=6 nodelay;
     limit_conn conn_limit_per_ip 3;
     try_files $uri $uri/ /index.html$is_args$args;
     root /home/hackman/www/example.com;
     index index.htm index.html;
 }
```

You must remove limits for static content:
```bash
location ~* ^.+.(jpg|jpeg|gif|png|svg|ico|css|less|xml|html?|swf|js|ttf)$ {
     root /home/hackman/www/example.com;
     expires 10y;
 }
 ```

 # Limit requests by User Agent

 As search engine indexing bots are getting more and more intelligent and thus more aggressive, sometimes they become really annoying or even can affect the performance of the system.

 While Nginx is a very powerful and flexible system, it is not always clear how to put all the configuration together to do the job.

 For any rate limiting, Nginx uses the `ngx_http_limit_req_module` module and it is pretty much strait-forward to limit based on IP address or any other simple value, but for the advanced configuration, you need to use maps with either static keys or regexp. That’s where things are getting more confusing.

 For clarity, and a more extended solution, let’s assume we want to limit user agents that match (GoogleBot|bingbot|YandexBot|mj12bot) pattern to 1 request from IP per minute burstable to 2 and the rest of the world to 10 requests per IP per second burstable to 15. To do this, the http section of the nginx.conf has to have the following part:
```bash
map $http_user_agent $isbot_ua {
        default 0;
        ~*(GoogleBot|bingbot|YandexBot|mj12bot) 1;
}
map $isbot_ua $limit_bot {
        0       "";
        1       $binary_remote_addr;
}

limit_req_zone $limit_bot zone=bots:10m rate=1r/m;
limit_req_zone $binary_remote_addr zone=one:10m rate=10r/s;

limit_req zone=bots burst=2 nodelay;
limit_req zone=one burst=15 nodelay;
```
The trick here is that we need to use two maps where the first one sets a value 0 based on the $http_user_agent and the second one sets the empty value for everyone who got 0 in the first map, but $binary_remote_addr for the ones who got the value 1 in the same first map. The idea is that for Nginx whitelist the request from limit zone, the return key and value from the map have to be empty (0 for key and “” for value), so the first map sets 0 for the value, and the second map takes that value as it’s key and sets the “” value.

Or you can use the below configuration:
```bash
 http {

     map $http_user_agent $limit_bots {
         default '';
         ~*(google|bing|yandex|msnbot) $binary_remote_addr;
     }

     limit_req_zone $limit_bots zone=bots:10m rate=1r/m;

     server {
         location / {
             limit_req zone=bots burst=5 nodelay;
         }
     }
 }
```

The rest of the configuration parameters are pretty much easy to understand and I won’t cover them here, since you can easily refer to nginx documentation.

To make things even nicer, we can also tell nginx to send a good HTTP 429 code (Too Many Requests) when someone is above the limit and hope that the requester will interpret accordingly and slow down. To make this, just add the following line in the same part of nginx configuration:
```bash
limit_req_status 429;
```

If you are using the limit_conn directive anywhere for nginx, you can add the same thing for it as well:
```bash
limit_conn_status 429;
```

Hope the above will save me and maybe even someone else some time and more similar posts to come later as I am getting my hands on different things.

 Sources:

- [ngx_http_limit_conn_module](http://nginx.org/en/docs/http/ngx_http_limit_conn_module.html)
- [ngx_http_limit_req_module](http://nginx.org/en/docs/http/ngx_http_limit_req_module.html)

