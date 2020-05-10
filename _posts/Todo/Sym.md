---
layout: post
title: Symfonos6 – Try Hack Me
subtitle: Walkthrough
tags: []
---

[Challenge](https://tryhackme.com/room/symfonos6)

## Task 1 -> Intro

Initiate the VPN connection and deploy the machine

We start by adding the IP address of our machine to the /etc/hosts

~~~
echo "10.10.124.168 sym" > /etc/hosts
~~~


Nmap scan to discover what we are working with

~~~
nmap -sV -T4 sym
~~~

![nmap](/img/2020-05-09-Sym/nmap.png)