---
layout: post
title: Running a Business as a Risk-Averse Introvert
---

![introvert startup founder cowering in front of his laptop](/assets/images/introvert.jpeg)

I have absolutely nothing at risk with my latest product. I still hold down a full-time job, spend time with my family and I don't work late into the night (which would risk burn out). If the business dies overnight I lose nothing (except some time invested).

Being an indie hacker (not hunting VC money and hockey-stick growth) gives me that option. I also believe it means I'm making a better product. Because there's no time pressure, I can let hard problems work themselves over in my head until the next day.

I've always been risk-averse but I've also always been creative, driven and entrepreneurial. Those things don't normally go in the same sentence but it is absolutely possible to have both. There are a few things that I've done to de-risk my side project so that I feel good about working on it and am not curled up in a stressed mess every night.

## Kept the scope as simple as possible

PriceWell is deliberately a simple application. I didn't set out to build something with a huge feature set. This has two big advantages.

1. I don't have to maintain too much code. This means customer support is kept to a minimum
2. I was able to ship the first version in a month and it's very easy to add new features

## Keep costs to a minimum

The only bills are hosting and analytics. Everything else either fits in the free tier of another service (zapier, HubSpot, Crisp etc) or uses open source software (Hugo for the marketing and help sites)

## Find free, sustainable marketing channels

I don't run adverts or pay influencers. We focused on two things from the beginning:

- SEO
- Answering questions on Reddit, Indie Hackers and Twitter

These marketing methods are sustainable and SEO actually builds over time of you keep working at it.

We've also been able to get listed in as many directories as possible which has the double benefit of

## Write the core business logic, defer everything else

This is also the core idea that lead me to build [PriceWell](https://pricewell.com?utm_source=introvert) in the first place. Billing shouldn't be something you have to maintain yourself. The same for authentication, we use [keycloak](https://www.keycloak.org/). It's as simple as deploying the open source software to a server. We use Google cloud for all our hosting and let them manage server capacity and manage the database. This means I don't have to troubleshoot anything except the core application code. I don't have to be a sysadmin which is another job off my plate. After all, I am the head developer, head of marketing, head of customer support, head of sales and head of finance, head janitor...
