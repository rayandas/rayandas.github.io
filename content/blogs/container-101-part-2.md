+++
date = '2020-08-29T18:52:28+05:30'
draft = false
title = 'Container 101 Part 2'
+++

### Build, Run, and Test a Container Image

Checkout my [Container 101 Part 1](https://rayandas.in/blogs/container-101/) blog.

In this part, let's start with a pre-built image that someone else has created and pulling that from a public registry. 

A registry is simply a collection or a repository of images and a public one is when it's made available to all people over the internet. 

To pull an image from a registry, whether that'd be a public registry or a private registry, we simple use the docker command along with the pull sub command.

I have a few images already pulled down from the docker hub, which is a public image registry.
![](/images/container-101-2/carbon.png)

Now I will run docker pull and I will specify the name of the image. And Because I'm not specifying a particular registry here, docker is going to default to docker hub, which is their public registry.
![](/images/container-101-2/carbon1.png)

Now let's do a docker image ls
![](/images/container-101-2/carbon2.png)

You can see the image is here. So now we can easily run a container based on this image.

Note: It's not necessary to pull down an image before you can run a container based on that image. If you try to run a container based on image that doesn't exist on your system, docker will simple pull it automatically from docker hub. 

The one problem is pre-built images, such as the one that I shown you is that we really dont know how that image was created. It's entirely possible that this image might contain some malicious software, or other files that we don't want or we dont't need. 

Now in some cases like with this simple alpine image, it's reasonably easy to verify what this image contains and how it was built. 

Now let's build an image from a Dockerfile:
![](/images/container-101-2/carbon3.png)

You can see that the docker image is built form the Dockerfile.

Now let's find the image and run it.

![](/images/container-101-2/carbon4.png)

So I have shown you how to pull down pre-built images and we have seen how to create custom images using some other image as a base or a starting point. 


Now we can distribute the images using a registry. Typically when you build a custom image, you're going to use that on more than just the system that you built it on, you're going to want to distribute it to other systems in your environment so that they can all run that image. That's part of what makes using containers to distribute software so useful as it's easy to distribute these images, which are also typically very small. 


