---
layout: post
title: Spring Cloud @FeignClient name as property
---

I've been using the fantastic [Spring Cloud Netflix](http://cloud.spring.io/spring-cloud-netflix/) a lot recently during a project to migrate a monolith to microservices. I spent some time recently writing a set of Selenium integration tests using Sorin Costea's excellent [example project](https://github.com/sorin-costea/bdd). I found myself wanting to run multiple Spring Boot microservices locally in order to run the Selenium tests. I wanted to run one service in particular locally but use Eureka for the others.

###Disabling Eureka For a Service

According to the [docs](http://projects.spring.io/spring-cloud/spring-cloud.html#spring-cloud-ribbon-without-eureka) you simply need to set `ribbon.listOfServers` for the service you want to point to locally. However I found this wasn't enough, after much searching, here's the final working configuration.

```
servicename:
  ribbon:
    eureka:
        enabled: false
    NIWSServerListClassName: com.netflix.loadbalancer.ConfigurationBasedServerList
    listOfServers: localhost:7000
```


This [configures Ribbon](http://cloud.spring.io/spring-cloud-netflix/spring-cloud-netflix.html#_customizing_the_ribbon_client_using_properties) to use your specified server list instead of those configured in Eureka.