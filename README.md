First what i did is scan by nmap
```
Starting Nmap 7.93 ( https://nmap.org ) at 2023-10-19 21:48 CEST
Nmap scan report for 10.10.10.194
Host is up (0.12s latency).
Not shown: 997 closed tcp ports (conn-refused)
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.2p1 Ubuntu 4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 453c341435562395d6834e26dec65bd9 (RSA)
|   256 89793a9c88b05cce4b79b102234b44a6 (ECDSA)
|_  256 1ee7b955dd258f7256e88e65d519b08d (ED25519)
80/tcp   open  http    Apache httpd 2.4.41 ((Ubuntu))
|_http-title: Mega Hosting
|_http-server-header: Apache/2.4.41 (Ubuntu)
8080/tcp open  http    Apache Tomcat
|_http-title: Apache Tomcat
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
``` 
We can see on port 8080 tomcat, intuition told me there will be vuln :P
But what i did is check the port 80, did small manual recon. I found this in source code, we need add this into /etc/hosts ```<li><a href="http://megahosting.htb/news.php?file=statement">News</a></li>``` Thne let's go check what on the domain. First thought what's come to mind is LFI, i think the ?file can be vulnerability. Turn on the burp and intercept traffic. And that how i say, there was a LFI, i got /etc/passwd

![image](https://github.com/Anogota/Tabby/assets/143951834/b8443ca3-ed3c-4670-af3d-59272b0e7d5e)

