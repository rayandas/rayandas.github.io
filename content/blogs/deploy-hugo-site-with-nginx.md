+++
date = '2020-06-04T11:31:15+05:30'
draft = false
title = 'Deploy Hugo Site With NGINX'
+++
![](/images/n+hugo.png)

I have just got an Ubuntu instance today. I am so excited to tinker around it. So I thought why don't I host my website and blog from my server instead of deploying it on Netlify. 

I struggled a little, but find a way through it. I will take you to the process step by step. 

### Prerequisites
* Linux OS: I recommend a dedicated system for hosting (VPS on a provider such as [DigitalOcean](https://www.digitalocean.com/products/droplets/), [Linode](https://www.linode.com/pricing/) or [Vultr](https://www.vultr.com/products/cloud-compute/)).
* A domain: You can't really expect to run a website without one. There is plenty of registrars out there. I personally like [NameCheap](https://www.namecheap.com/).

### Installing Hugo
Visit the [Hugo quickstart guid](https://gohugo.io/getting-started/installing/#debian-and-ubuntu) for destro specific information. I installed Hugo on my Ubuntu server with 
```bash
sudo apt install hugo
```
If Hugo is not in your distro’s repositories, you can always download it with the [tarball](https://gohugo.io/getting-started/installing/#install-hugo-from-tarball).

### Configure Nginx
I hope you built your site locally and pushed to GitHub. If not, refer to my blog [Start Your Blog With Hugo](https://rayandas.in/blogs/start-your-blog-with-hugo/).

Now make sure you have installed Nginx, which is available on pretty much default repository. 

Now we are going to create a configuration file for our site. 
```bash
cd /etc/nginx/sites-available/
sudo vim hugo-site
```
I hope you know how to use Vim. 

Now your configuration should look like this:
```bash
server {

        listen 80;
	listen [::]:80;
	server_name example.in www.example.in;
        return 301 https://example.in$request_uri;
}

server {

	listen 80;
        listen [::]:80;
        
	server_name example.in;

        root /home/username/hugo/public/; #Absolute path to where your hugo site is
        index index.html index.htm index.shtml; # Hugo generates HTML

        location / {
       		try_files $uri $uri/ /index.html =404;
       }
}

server {

        listen 80;
        listen [::]:80;

        server_name www.example.in;

        root /home/username/hugo/public/; #Absolute path to where your hugo site is
        index index.html index.htm index.shtml; # Hugo generates HTML

        location / {
        	try_files $uri $uri/ /index.html =404;
        }
}
```

To enable this site, we need to create a symlink from your site into `site-enabled`.
Use absolute paths to avoid symlink confusion.
```bash
sudo ln -s /etc/nginx/sites-available/hugo-site /etc/nginx/sites-enabled/hugo-site
```

Now we can start and enable Nginx with the following commands:
```bash
sudo systemctl start nginx
sudo systemctl enable nginx
```

### Quick Checks
* Did you add registrars nameservers to point at the server you’re using to host?
* Did you create A records with your hosting provider to direct requests to the correct server? (add a separate A record for the www subdomain)

### Add SSL Certificates
SSL is a must these days, and it’s very easy to implement. I used [Certbot](https://certbot.eff.org/), because it's easy to use and hey, who doesn't love the [EFF](https://www.eff.org/)?

Visit the certbot site to get customized instructions based on your setup, but here is the process for NGINX running on Ubuntu:

First we'll add the certbot PPA:
```bash
sudo apt-get update
sudo apt-get install software-properties-common
sudo add-apt-repository universe
sudo add-apt-repository ppa:certbot/certbot
```

Then we'll install certbot itself:
```bash
sudo apt-get install certbot python-certbot-nginx
```

And finally, we'll run the setup script:
```bash
sudo certbot --nginx
```

Now check your website. Yay congratulations. \o/


