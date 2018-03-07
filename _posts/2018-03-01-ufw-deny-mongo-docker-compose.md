---
layout: post
title: Ufw Deny Mongodb Using Docker Compose
---

## The problem

I moved the infrastructure of [cronasaservice.com](https://www.cronasaservice.com) to a new hosting provider recently. A few days after the move I received a strange email (thank you German security services).

```
Dear Sir or Madam,

MongoDB is a popular NoSQL database system commonly used as a backend
for web applications. Access to a MongoDB server should be restricted
to trusted systems (for example, the related web application server).
If a MongoDB server is openly accessible from the Internet, an attacker
can take advantage of this to access the server and modify or delete
data, or even obtain sensitive information like customer data from
an online shop.

Affected systems on your network:

 Format: ASN | IP   | Timestamp (UTC) | Mongodb version
         xxx | xxxx | xxx             | x.x.x

We would like to ask you to check this issue and take appropriate
steps to secure the MongoDB servers on the affected systems or notify
 your customers accordingly.
```

I found this strange as had (configured UFW)[https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-with-ufw-on-ubuntu-14-04] to block everything except port 80. I ran a few port scanners and sure enough the mongodb port **27017** was open.

After some googling, it seemed a few people were having the same issue. It turns out Docker was the culprit here. It was overriding the UFW rules to set it's own iptables rules. Luckily the fix is pretty simple.

## Solution

To stop Docker overwriting the iptables, simply edit `etc/default/docker`.
Uncomment the following line:
`#DOCKER_OPTS=...`

and add `--iptables=false`

The result should be: 

`DOCKER_OPTS="--dns 8.8.8.8 --dns 8.8.4.4 --iptables=false" `

Next, restart docker using `service docker restart`.

You might need to restart some docker containers at this point (I did as I was using Docker Compose).