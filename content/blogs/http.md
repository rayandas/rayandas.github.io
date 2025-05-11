+++
date = '2020-09-20T12:25:38+05:30'
draft = false
title = "Your Browser's Language: HTTP"
+++

Ever wondered what actually happens when you type an address into your web browser and then hit enter?
At that moment your computer starts talking to another computer, called the server, which is usually thousands of miles away. And in milliseconds your computer asks that server for a website and that server starts to talk back to your computer in a language called HTTP. 

HTTP stands for HyperText Transfer Protocol. You can think of it as the language that one computer uses to ask another computer for a document. 

If you were to intercept the conversation between your computer and a web server on the internet, it's mainly made up of something called `GET` requests. Those are really very simply the word GET and the name of your document that you are requesting. 

Example of what an HTTP request looks like:
```bash
GET document-name HTTP/1.1
Host: website-name.com
User-Agent: curl
Accept: */*
```

Example of what an HTTP response looks like:
```bash
HTTP/1.1 200 OK
Cache-Control: max-age=31536000
Content-Type: text/html
...
<!DOCTYPE html>
...
```
Now sometimes when you browse the web, you're not just requesting documents with `GET` requests. Sometimes you sent information like when you fill out a form or type a search query, your browser sends this information in plain text to the web server using an `HTTP POST` request. 
Example:
```bash
POST /search HTTP/1.1
Query=Batman+images
```
Let's say you log in to a website. The first thing you do is you make a `POST` request, which is a POST to the website's login page that has some data attached to it. It has your email address, your password. That goes to the website's server, the server figures out that okay, you are John. Now it sends a web page back to your browser that says, Successfully logged in as John. But along with that web page, it also attaches invisible cookie data that your browser sees and knows where to save. 

The cookie is really important because it's the only way that a website can remember who you are. That cookie data is like an ID card for the website. It's a number or something that identifies you as John. Your web browser holds on to that cookie data and the next time you revisit the website, your web browser knows to automatically attach that cookie data with the request that it sends over to the website's server. So now the website's server sees the request coming from your browser, sees the cookie data, and knows "okay, this is the request from John".


