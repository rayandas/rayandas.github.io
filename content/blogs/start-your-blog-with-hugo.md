+++
date = '2020-05-23T20:06:13+05:30'
draft = false
title = 'Start Your Blog With Hugo'
+++
A detailed steps to start your own blog site using Hugo from zero to deployment.

Hugo is one of the most popular open-source static site generators. With its amazing speed and flexibility, Hugo makes building websites fun again.

I love Hugo because it's fast, is has Go at the core. Install in seconds, build in milliseconds. Hugo works on macOS, Windows, Linux, FreeBSD, and others. Host on any server or your favorite CDN. 

Hugo is amazing, especially if you are a developer and you’re willing to write in Markdown. Non-tech people might just refuse to use Markdown, and it’s perfectly understandable.

Also, you have to be prepared for a Git-centric workflow to make things really quick.

Anyway, enough with words.

What you do is that you write a post using Markdown, then commit your changes to a Git repository, most commonly on GitHub, and some glue technology deploys the changes on the server that hosts the site.

### Install Hugo
Mac OS:
```bash
$ brew install hugo
```
If you don't have brew on your Mac install [Homebrew](https://brew.sh/)
Linux:
```bash
$ snap install hugo
```
Windows:
```bash
$ choco install hugo -confirm
```

### Create a Hugo Site
Once Hugo is installed, create a hugo site by running 
```bash
$ hugo new site hugo-blog
```
The command will create a new `hugo-blog` directory.

### Time to Pick a Theme
You need to pick a theme before you can start. You can find all the themes [here](https://themes.gohugo.io/).
I have used [Etch](https://themes.gohugo.io/etch/)
I will recommend avoiding the `git clone` workflow they suggest on the page, because you can modify the theme according to you in the future. Better to fork the theme and use the forked repository in your hugo site. 

So go to your forked repository, copy `git@github.com:username/theme.git` and add it as a submodule under `themes` dir. 
```bash
$ git submodule add https://github.com/username/theme.git
```

### Add Content to Your Blog
In this step we'll add content to our blog. Hugo simplify this process.
To add content in blog page:
```bash
$ hugo new posts/first-post.md
```
The newly created content file will start like this
```bash
---
title: "First Post"
date: 2020-08-02T08:47:11+01:00
draft: true
---
```

### The Configuration
To configure Hugo we use a configuration file. That file is located in our Hugo site root dir and can be in TOLM (config.toml), YAML (config.yaml) or JSON (config.json) format.

The config.toml in my case looks like 
```bash
baseURL = "https://rayandas.in/"
languageCode = "en-us"
title = "Rayan Das"
theme = "etch"
enableInlineShortcodes = true
pygmentsCodeFences = true
pygmentsUseClasses = true

[params]
  description = "Personal web space."
  copyright = "Copyright © 2020 Rayan Das"
  dark = "off"
  highlight = true

[menu]
  [[menu.main]]
    identifier = "blogs"
    name = "blogs"
    title = "blogs"
    url = "/blogs/"
    weight = 10

[permalinks]
  posts = "/:title/"

[markup.goldmark.renderer]
  # Allows HTML in Markdown
  unsafe = true
```
I recommend you to configure is as per your requirement.

### Run the Server

Now that we've configured almost everything, we will run the server.
```bash
$ hugo server
```

The site is running on your localhost now. Open `http://localhost:1313` in your browser to see the site.

If everything works well, congratulations. Your site is up!

### Configure Hugo Version in Netlify
You need to set Hugo version for your environments in `netlify.toml` file.
The Netlify configuration file can be a little hard to understand and get right for the different environment, and you may get some inspiration and tips from this site’s `netlify.toml`:

```bash
[build]
publish = "public"
command = "hugo --gc --minify"

[context.production.environment]
HUGO_VERSION = "0.74.3"
HUGO_ENV = "production"
HUGO_ENABLEGITINFO = "true"

[context.split1]
command = "hugo --gc --minify --enableGitInfo"

[context.split1.environment]
HUGO_VERSION = "0.74.3"
HUGO_ENV = "production"

[context.deploy-preview]
command = "hugo --gc --minify --buildFuture -b $DEPLOY_PRIME_URL"

[context.deploy-preview.environment]
HUGO_VERSION = "0.74.3"

[context.branch-deploy]
command = "hugo --gc --minify -b $DEPLOY_PRIME_URL"

[context.branch-deploy.environment]
HUGO_VERSION = "0.74.3"

[context.next.environment]
HUGO_ENABLEGITINFO = "true"
```

### Deploy your Hugo Site on netlify

First, you need to create a GitHub repository and push everything to the repository. You can keep the repo private, ofcourse. 

Once the repo is on GitHub, we can move to Netlify. From the Netlify dashboard, click the 'New site from GitHub' button. 

Click GitHub, authorized Netlify to access your private repositories, then pick the repo you just created. Netlify automatically identified it as a Hugo repo, and entered the build command automatically.

Selecting “Deploy site” will immediately take you to a terminal for your build. Once the build is finished—this should only take a few seconds. 
 
Now every time you push changes to your hosted git repository, Netlify will rebuild and redeploy your site.


### Have Fun 
The best way to learn something is to play with it.

