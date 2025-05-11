+++
date = '2020-09-16T22:37:16+05:30'
draft = false
title = 'The Twelve-Factor App'
+++

## Introduction

In the modern era, a software is commonly delivered as a service, called `web apps` or `software-as-a-service`. The twelve-factor app is a methodology for building software-as-a-service apps.

I intend to summarise the twelve-factor app as a set of bullet points: 

1. Codebase - Single codebase and that codebase is not shared between apps.
2. Dependencies - Manage its dependencies completely and explicitly.
3. Configuration - Keeps config out of the code, prefers environment variables and setting values per deploy.
4. Backing services - views all other services as backing services, whether they’re in-house or third party.
5. Build, release and run - These states are strictly separated from each other. 
6. Processes - Given that processes can disappear at any moment, all processes should be stateless.
7. Port binding - self-contained and self-sufficient, requiring no runtime injection and exposing itself on a port.
8. Concurrency - Applications need to be able to scale horizontally, so there might be more than one instance of the service running at a time. 
9. Disposibility - Processes are completely disposable as they are quick to start up and graceful to pull down.
10. Environment parity - The application should at all times work on all environments (development, production, etc) and environments should be as similar as possible.
11. Logs - Logs should be output to stdout and stderr and one should use some external tool for handling logs.
12. Admin processes - These should run as one-off processes, in an environment identical to the one in which the application is running.

Read more about each point in more details in [The Twelve-Factor App](https://12factor.net)
