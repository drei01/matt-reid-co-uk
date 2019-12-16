---
layout: post
title: docker-compose npm install hangs
---

## getaddrinfo EAI_AGAIN registry.npmjs.org

I use a two step process for deploying changes to one of my apps, first `docker-compose build app` to build the latest image and then `docker-compose up --no-deps -d app` to replace the current version.

Recently the first step in this process started hanging at the line `RUN npm install`. After much research, this appears to be a DNS issue. I tried all the suggested fixes, restarting docker and the machine itself but nothing helped. I could ping the registry.npmjs.org from the machine itself, just not from docker. Finally, what worked was running docker in **host** mode (using the dns of the machine) during build.

## Make sure you have at least version 2.2 of docker-compose

Check out the [releases](https://github.com/docker/compose/releases) page if you need to upgrade.

## Set network to host

Make a change to the *build* section of your `docker-compose.yml`

``` yaml
    build:
      network: host
      context: .
```

Now you can run `docker-compose build app` using the host network.

## If docker-compose won't start using the host network

In my case, the image now built fine but running `docker-compose up --no-deps -d app` resulted in an error that the host network doesn't work with links. The solution here is to remove the "network: host" line, run the build step again (it will use the cache so npm install will work) and then run the `up` command.
