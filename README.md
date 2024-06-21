# Boardlight-walkthrough
 

# Exploration

We start with nmap scanning.
The Nmap scan reveals two open TCP ports: port 22, which runs 
OpenSSH, and port 80, which hosts an Apache web server

```bash
nmap -sC -sV -Pn -v -A 10.10.11.11
```

![alt text](https://github.com/Milamagof/boardlight-walkthrough/blob/fd2a4a93d2c557f009cc9f16c7b231e46e546f32/1.jpg)

Navigating to the website on 10.10.11.11, we find the home page of
the website.
Nmap also gave us the hostname Board.htb.

![alt text](https://github.com/Milamagof/boardlight-walkthrough/blob/fd2a4a93d2c557f009cc9f16c7b231e46e546f32/2.jpg)

We can try to find subdomains with wfuzz.
```bash
wfuzz -c --hc 400,404 -t 200 -w dictionary.txt -u http://board.htb -H "Host: FUZZ.board.htb"
```
 
![alt text](https://github.com/Milamagof/boardlight-walkthrough/blob/fd2a4a93d2c557f009cc9f16c7b231e46e546f32/3.jpg)

We find the new domain crm.board.htb

![alt text](https://github.com/Milamagof/boardlight-walkthrough/blob/fd2a4a93d2c557f009cc9f16c7b231e46e546f32/4.jpg)

We find a login page and the name and version of what is running
behind Dolibarr 17.0.0.

[CVE-2023-30253](https://github.com/nikn0laty/Exploit-for-Dolibarr-17.0.0-CVE-2023-30253.git) 

it was very easy to find an exploit

The script works, thanks to a default username and password I
found
![alt text](https://github.com/Milamagof/boardlight-walkthrough/blob/fd2a4a93d2c557f009cc9f16c7b231e46e546f32/19.jpg)

![alt text](https://github.com/Milamagof/boardlight-walkthrough/blob/fd2a4a93d2c557f009cc9f16c7b231e46e546f32/6.jpg)

Once inside, I spent quite a while going through the directories, looking for something that would help me. 
A username and password.

![alt text](https://github.com/Milamagof/boardlight-walkthrough/blob/fd2a4a93d2c557f009cc9f16c7b231e46e546f32/7.jpg)

It took me a while to figure out how to use the password, but I remembered that I had found a user larissa and that was the way.

![alt text](https://github.com/Milamagof/boardlight-walkthrough/blob/fd2a4a93d2c557f009cc9f16c7b231e46e546f32/8.jpg)

there was the user flag
![alt text](https://github.com/Milamagof/boardlight-walkthrough/blob/fd2a4a93d2c557f009cc9f16c7b231e46e546f32/18.jpg)


# Privilege escalation

we will use linpeas.sh

![alt text](https://github.com/Milamagof/boardlight-walkthrough/blob/fd2a4a93d2c557f009cc9f16c7b231e46e546f32/12.jpg)

![alt text](https://github.com/Milamagof/boardlight-walkthrough/blob/fd2a4a93d2c557f009cc9f16c7b231e46e546f32/11.jpg)

I had to investigate everything linpeas gave me, and I found
that there was an exploit for the SUID binaries

![alt text](https://github.com/Milamagof/boardlight-walkthrough/blob/fd2a4a93d2c557f009cc9f16c7b231e46e546f32/13.jpg)

After cloning the repository and transferring the exploit script to the
target machine we look for root

![alt text](https://github.com/Milamagof/boardlight-walkthrough/blob/fd2a4a93d2c557f009cc9f16c7b231e46e546f32/14.jpg)

![alt text](https://github.com/Milamagof/boardlight-walkthrough/blob/fd2a4a93d2c557f009cc9f16c7b231e46e546f32/15.jpg)

![alt text](https://github.com/Milamagof/boardlight-walkthrough/blob/fd2a4a93d2c557f009cc9f16c7b231e46e546f32/16.jpg)


# Root flag

![alt text](https://github.com/Milamagof/boardlight-walkthrough/blob/fd2a4a93d2c557f009cc9f16c7b231e46e546f32/17.jpg)

