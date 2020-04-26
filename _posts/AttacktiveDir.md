---
layout: post
title: Attacktive Directory – Try Hack Me
subtitle: Walkthrough
tags: [active,directory]
---

## Task 1

Initiate the VPN connection and deploy the machine

## Task 2 => Impacket

Install Impacket, this is a collection of Python classes for working with network protocols. More information can be found [here](https://www.secureauth.com/labs/open-source-tools/impacket). 
Have a look at (this)[https://github.com/SecureAuthCorp/impacket.git] Github repository to learn how to install it.

## Task 3 => Enumeration 1

We start by adding the IP address of our machine to the /etc/hosts

~~~
echo 10.10.194.183 spookysec.local >> /etc/hosts
~~~

Basic nmap scan to discover what we are working with

~~~
nmap spookysec.local
~~~
