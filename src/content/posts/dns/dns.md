---
title: About DNS
published: 2025-08-26
author: 'Choker'
description: Some details for Domain Name System
image: 'https://tryhackme-images.s3.amazonaws.com/room-icons/66704dd0e54a1f39bff7b1a1-1735573839890'
tags: ["DNS", "Web"]
category: 'Choker'
draft: false
---


## Definition of DNS


DNS(Domain Name System) is a convinient system for users to communicate with internet without rememebering IP Address.
Before DNS used, When we wants to connect with websites, we need IP address.
For example, we usually type `www.google.com` to access to Google.
But, If there's no DNS, we need to  type `8.8.8.8` to log in Google.

## Hierarchy of DNS

### TLD
TLD(Top-Level Domain) is the most righthand part of the domain. For example, `www.google.com`'s `.com` is TLD.
There's 2 parts in TLD, which called **gTLD** and **ccTLD**. gTLD(Generic Top Level Domain) means the purpose of website. `.com` is for commercial purpose, `.net` is for network-related website, etc. ccTLD(Country Code Top Level Domain) means the geographical purpose of the website. Like `.us` is for USA, `.jp` is for Japan.
Now, There's very variable gTLD. you can visit [here](https://data.iana.org/TLD/tlds-alpha-by-domain.txt) to see those gTLDs.

### Second-Level Domain
Second-Level Domain is second part (from right) of the domain. `www.google.com`'s `google` is it.
Second-Level Domain has limit to be named. It must be under 63 characters and TLD. Also, only a-z, 0-9 and hyphens are available. But hyphens cannot be placed start or end of it and used consecutive.


### Subdomain
Subdomain is most lefthand part of the domain. `en.wikipedia.org`'s `en` is it.
The limitaion of subdomain is same as Second-Level Domain.
Multiple subdomains are available unlike other domain, but it has to be under 253 characters.
If there's no subdomain, it called `Apex Domain`. In this case, `www` goes front of it.

## Record Types of DNS

### A Record
This record resolves to IPv4.

### AAAA Record
This record resolves to IPv6.

### CNAME Record
This record resolve to another domain.
For example, domain firstexample.com returns CNAME record secondexample.com.
But, as they don't return Ip address, secondexample.com request Ip address.

### MX Record
This record resolve address of the server where to send an email.
If firstexample.com's server goes down, MX record resolve secondexample.com's address(like back-up server) to send an email.

### TXT Record
This record is free field where can store any text-based data.
It can be used in many ways. Like list servers that user wants to get an email from, or verifying in third-party services.

## Process of DNS

### 1. Check Cache
If user request domain name, computer checks user's local cache to find previous looked-up address.
If there is it, goes to 4.

### 2. Recursive Server
Recursive server is usually provided by ISP. But, user can choose if he want.
Recursive Server also find previous looked-up address.
If there is it, goes to 4.

### 3. Root Server
If local and Recursive server doesn't have address, computer goes to root server.
In root server, They redirect you to TLD.

### 4. TLD Server
In TLD server, they records where to find authoritative server(= name server) to answer the DNS request.

### 5. Authoritative Server
This server restore DNS record. DNS record sent domain to Recursive server and they sent to local cache.(Step 1,2)
After all, they sent it to user.
In this part, every DNS record has TTL(Time To Live), which is a time to store response until user look for it again.


## Finishing
You can test these in cmd.

```bash
nslookup --type=CNAME xxx.com
```

Try command like these.

