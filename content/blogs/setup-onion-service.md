+++
date = '2020-12-24T00:19:25+05:30'
draft = false
title = 'Set Up An Onion Service For Your Website'
+++
![](/images/setup-onion-1.jpg "Image Source: https://www.torproject.org/")

When looking to remain anonymous in today's world, [Tor](https://www.torproject.org) is your safest bet. The Tor browser is a powerful free tool used for browsing the Internet anonymously, where you can discover varying websites utilizing the onion domain.

Anonymity is seemingly fading nowadays with ISPs watching your every move and big tech websites selling off your information data to the highest bidder. If you are looking to create a new website, or even if you happen to already own one, it may be worth looking into what an onion site can offer you in terms of site protection for both yourself and your visitors.

[Download Tor Browser](https://www.torproject.org/download/).

## What Is An Onion Domain?

An onion domain is an IP suffix that is exclusively for use through the Tor anonymity browser. This means that standard browsers like Microsoft Edge, Google Chrome, and Mozilla Firefox will not have access to sites using the onion domain as they are unable to navigate [the relay of Tor proxy](https://www.eff.org/pages/what-tor-relay) from which Tor is created.

## Set Up Your Onion Service:

* Get a working Tor:
Here is the [Tor installation guide](https://community.torproject.org/onion-services/setup/install/).

* Get a web server working:
Assuming that you are already running `nginx` or `apache` on port `80` of your server. 

* Configure your Tor onion service:
Open the `/etc/tor/torrc` and add the following two lines.

```bash
HiddenServiceDir /var/lib/tor/my_website/
HiddenServicePort 80 127.0.0.1:80
```
Now restart the `tor` service.
```bash
sudo systemctl restart tor
```

When Tor restarts, it will automatically create the  HiddenServiceDir  that you specified. Make sure this is the case.

Now we can see the address from the hostname file.
```bash
cat /var/lib/tor/my_website/hostname
hgxzzsqdli44o5wn7z3zo7djjfi7snhawqea6vzwgyad7uizmxqw6gyd.onion
```
It will also create a `authorized_clients` directory at the service directory.

Next step is to create keys of type `x25519` You can use these implementations. 
1. [Python](https://github.com/pastly/python-snippits/blob/master/src/tor/x25519-gen.py)
2. [Rust](https://github.com/ppopth/torkeygen)
3. [Bash](https://gist.github.com/mtigas/9c2386adf65345be34045dace134140b)

I got the secret and the public key using the Python implementation.
```bash
public:  4A4SE2S3YXLR35K57D3EXVQKFW2WNVFCDMZRBHIF4APLMKE3AF3Q
private: AF7ER763REDLRI2ID7VROVINIRZCFWQHQIFT4KVOWOQYZRXOUF3A
```

Now, we will use the public key to create a `clientname.auth` file in `/var/lib/tor/my_website/authorized_clients/` directory.
```bash
sudo vim /var/lib/tor/hidden_service/my_website/raydeeam.auth
```

Then we have to write as below (the file format is like `descriptor:x25519:public_key)`:
```bash
descriptor:x25519:4A4SE2S3YXLR35K57D3EXVQKFW2WNVFCDMZRBHIF4APLMKE3AF3Q
```

Now restart the `tor` service again.
```bash
sudo systemctl restart tor
```

## Configure Nginx:
Add `Onion-Location` header in your main `nginx` configuration.
```bash
# /etc/nginx/sites-enabled/example.conf

server {
    listen 80;
    server_name example.com;
    add_header Onion-Location http://hgxzzsqdli44o5wn7z3zo7djjfi7snhawqea6vzwgyad7uizmxqw6gyd.onion$request_uri;
    ...
    ...
}
```

Then Create another configuration file same as your main config file, remove your domain names and add the `.onion` hostname in `server_name`.
```bash
# /etc/nginx/sites-enabled/onionsite.conf

# Given a hidden service running at hgxzzsqdli44o5wn7z3zo7djjfi7snhawqea6vzwgyad7uizmxqw6gyd.onion,
# configured to connect to 127.0.0.1:80,
# an nginx site config for .onion hostname might look like below.

server {
    listen       80;
    server_name  hgxzzsqdli44o5wn7z3zo7djjfi7snhawqea6vzwgyad7uizmxqw6gyd.onion;
    rewrite ^/(.*) http://hgxzzsqdli44o5wn7z3zo7djjfi7snhawqea6vzwgyad7uizmxqw6gyd.onion/$1 permanent;
}
server {
    listen       80;
    server_name  hgxzzsqdli44o5wn7z3zo7djjfi7snhawqea6vzwgyad7uizmxqw6gyd.onion;
    ...
    ...
    location / {
        ...
    }
    ...
}
```

Now restart `nginx` and `tor` services.
```bash
sudo service nginx restart
sudo systemctl restart tor
```

References:

1. https://community.torproject.org/onion-services/setup/

2. https://kushaldas.in/posts/setting-up-authorized-v3-onion-services.html
