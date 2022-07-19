---
title: "Day 9: How to get your website out to the world!"
date: 2022-07-10
tags: []
draft: false
weight: 9
---

# Deployment

Until now we have created django application and run it on our own machine. We can see our web app running on our browser on `localhost:8000`. Now its time to dimystify what this localhost:8000 thing is. To understand this we first need to understand three concepts IP addresses, ports and DNS(Domain Name System). Lets go through them one by one

### IP Address

IP stands for internet protocol. Millions of computers interconnected forms internet this internt connection is the connection formed with wires(optical fibres) and wireless communication. Fun fact:there are submarine cables running throught oceans which carry this website's content from our server in US to you.

![](/attachments/bigimage.png)

When we exhange message in the internet, message may include video, text audio, It always has some sending computer and some receiving computer. so how does computer know whom to send the message to? Computers use numbers to identify each other in the internet. To make these numbers human readble they are written in the format `192.168.100.1`. it starts from `0.0.0.0` to `255.255.255.255` all the number in between these ranges are called IP address, IPv4 address to be more specific. So lets say when you are reading from the `locus.com.np` site
you were able to read this content because your computer asked some computer having address lets say `20.84.44.131` to send its content. So to get content from some website we need to memorize its IP address? not exactly this is where DNS come into the picture

### Domain Name System

Domain name system is the database which stores name to address mapping. Its because of DNS we dont need to memorize the IP address instead we only need to remember `locus.com.np` to communicate with the website. There are some computers in the internet which stores these mapping,so if we give them `locus.com.np` it will reply us back `20.84.44.131`. So each time we hit `locus.com.np` on our browser tab our browser will ask some pre-configured computer(DNS server) about its IP Address and when it replies back the IP address of that computer, we can send request for content to that IP address.

So we can imagine DNS server stores something like

### Tables

| Domain Name     | IP address     |
| --------------- | -------------- |
| locus.com.np    | `20.84.44.131` |
| classictech.com | `56.78.101.2`  |
| ...             | ...            |

### Port

To understand what port is , simply think that what we have talked till now is correct but not exactly. To talk with the computer we need to specify the IP address of that computer and additionallly to which port we want to talk to. Like IP port are also idenfified as number, computer can have port numbers ranging from `0` to `65535`. Simply think of port as department in the Organization and IP address as a Organization. In an organization we have to talk to different department for the different services, asking http message from the computer `20.84.44.131` on port `80` is analogous to asking for markettting related document to the marketting department in some orgarnization. But you may think, we are not specifying any port number when we are typing `locus.com.np` in the URL bar of our browser. So there is a trick. When you dont mention any port in the browser, port `80` is assumed by default.so `locus.com.np` and `locus.com.np:80` are exactly same thing. So port 80 is the default port for http protocol which is used to browse websites.

you can see list of other default ports [here](https://docs.oracle.com/en/storage/tape-storage/sl4000/slklg/default-port-numbers.html)

### So what does localhost:8000 mean?

localhost is domain name, it resolves into some IP, how does, there is a small catch here, our computer does not always ask remote dns server for resolving domain name into IP. There are some domain name that is resolved locally in our host itself. computer checks its own list of dns mapping before asking to remote dns server. this list looks something like.
`cat /etc/hosts` command in linux displays this local dns mappings.
![Pasted image 20220708190457.png](/attachments/Pasted%20image%2020220708190457.png)
In above picture we can see that localhost maps to `127.0.0.1`. And `127.0.0.1` is special IP Address which means to current host(your own computer), which means if i hit `127.0.0.1` on browser URL tab it will not try to connect to other remote computer but it will try to connect to itself. Think something like a company is trying to communicate with its internal department. Like every friend of yours refer to you by your name but you refer to yourself as "Me" in the software world `127.0.0.1` is used as "Me" by computers.

So we finally understand that `localhost:8000` in URL bar means connect to port `8000` of your own pc. And we could have specified different port while running our service (django in our example) like `python manage.py runserver 3000` this will start serving the web app in port `3000` and we could use `localhost:3000` in URL bar to connect to this django web app.

### URL Strucuture

lets take simple example URL `https://support.reddit.com`
`.com` ==> top level domain
`reddit` ==> second level domain
`support` ==> subomain
`https` ==> protocol

As shown above URL has strucuter and different part of the url mean different things. we will not go into detail here but its good to know. This is ofcourse simple url without paths and query parameters, you can learn more about urls [here](https://medium.com/@joseph.pyram/9-parts-of-a-url-that-you-should-know-89fea8e11713)

### Public Vs Private IP Address

Now you might assume the steps to deploy you site as, you can choose some name like `mycoolsite.com` and then access the database server where mapping for this domain is stored and then change the record to point to your computer's IP. So whats your computer IP? How to find it?

Unfortunately its slightly more complicated than that. You don't get Public IP you only get Private IP, Private IP are given to your PC by your routers. But to be globally accessible you need public IP. There are only limited IP address in the world (about 4 billion) so assigning this IP to every device is not possible so there is concept of private IP, public IP and subnetting. There are lots of resource in the internet to learn about these concepts we will not cover all of them in this course but [here](https://www.youtube.com/watch?v=po8ZFG0Xc4Q) is the starting point. In this course we only need to understand that you cannot point some domain to your computer's IP address and host your site in your own PC because your PC does not have Public IP address.

### Getting Your Own Server Ready

{{< youtube PB0cxKzJC-4 >}}

So now we know that to host our website we need computer with public IP address, how can we get computer with public IP adderss? Here comes the term known as IAAS(Infracture as a service), there are cloud service providers which provides computers in rent, we can buy computer from them and use as we want.. Buying these computer is like buying infrastructure so the service is called Infrastructure as a service. These computers are charged on the basis of time(like monthly) or usage(how much cpu and ram you use). These remote computer are also called Virtual Private Server (VPS) or Virtual Machine (VM). Microsoft's [Azure](https://azure.microsoft.com/en-us/) and Amazon's [AWS](https://aws.amazon.com/) are some providers that provide IAAS.

There are two major steps involved in getting your own VPS.

1. Sign in to your favourite VPS provider

1. Buy and create Virtual machine (1 cpu and 1gb ram linux machine will cost approx $10/yr)
   NOTE: Those who have their educational email can get $100 azure student credit
   this can be used to buy VPS with 1 CPU and 1GB ram for 1 approx 1 year.

   Buying and creating VPS is very easy, you just need to do some clicks. At the end you will download Private Key to access the server. Think of key just like key in normal life, you need this key to get access to your remote computer, keep it safe like you keep your room's key safe. Private key is a cryptography concept, to understand how it works [this](https://www.youtube.com/watch?v=wXB-V_Keiu8&t=361s) could be your starting point. In this course you just need to understand that to access your VPS you need your private key, before connecting to your VPS from your computer we will need to specify this key somehow, we will talk how you do that later.

1. Now after buying and creating a VPS we need to connect to this VPS somehow, since in this course we talk about linux virtual machine in the server we will connect to this virtual machine using `ssh`.

### Connecting and executing commands in your Virtual Machine

Now that you know how you have successfully created virtual machine, next step is use this machine. since we have created linux virtual machine, our goal is to get command line access to the machine, so that we can run commands, install software, and run our software in this virtual machine. Our virtual machine has its own IP Address. We will need three things to connect to this machine and get command line access, IP address of this remote virtual computer, key to access this server, software that will help us connect to this remote computer. we can get the IP address of the virtual machine from azure portal, private key is already downloaded into our virtual machine while cretating the server, the software we use is called `ssh`. know that `ssh` is the name of the protocol and also software.

Open your bash terminal and use `ssh -i <private key path> username@IP` command to connet to your virtual machine, it will look something like this.
![Pasted image 20220708223713.png](/attachments/Pasted%20image%2020220708223713.png)
Congratulations, you got command line access to the virtual machine, now you can type commands in your terminal, it will travel throught oceans to reach your virtual machine, will execute there and the output will return back to you through oceans again, isn't that magic? all this highlighted commands are executed in virtual machine.
![Pasted image 20220708224244.png](/attachments/Pasted%20image%2020220708224244.png)

### Hosting your site on the server

Now we need to somehow transfer our code to this server, this can be done using github, we can push the code in our local machine to the github and use git to pull this code from github to the remote virtual machine, by this way we will have access to the code in our server. Now we can install our dependencies and run our django app in the server. When we do that it will be globally accessible. remember how we used `localhost:8000` to access django website running on our own server. In similar manner we can access the web app running on our server by typing `http://IP:PORT` in our browser eg. `http://20.84.44.131:8000/` in the image below, `20.84.44.131` was the IP Address of my virtual machine which i obtained from azure portal, and in that virtual machine i cloned my django project and ran it by using `python manage.py runserver 0.0.0.0:8000` and now anyone in the world could access my site using `http://20.84.44.131:8000/` this link. Note that we used `0.0.0.0` instead of `localhost` this is because `localhost` and `0.0.0.0` are almost similar but there is one important difference, you can access `localhost` only from the same host(computer), but you can access the web server from other host if we run the web server at IP `0.0.0.0`
![Pasted image 20220708225003.png](/attachments/Pasted%20image%2020220708225003.png)

### How to buy domain name? is it free?

To point the domain of your choice `mycoolsite.com` to some computer we want, you need to access the dns entry for that domain. There are a lot of services that let you buy domain name and change its IP address entry to point to your server, example of such service provider is [Namecheap](https://www.namecheap.com/). You can buy your domain from such site and change the record for your domain name to point to your server PC. I brought `locus.com.np` and changed its entry to point to the IP address `20.84.44.131`. After waiting for some time now i can access my site as
![Pasted image 20220708225827.png](/attachments/Pasted%20image%2020220708225827.png)

To add domain to IP mapping is very easy, you just goto the dash board of your domain name provider and add two records
![Pasted image 20220708230630.png](/attachments/Pasted%20image%2020220708230630.png)

Above image was my admin pannel for the domain `botsworld.me` in Namecheap.There are just two record you need to add to configure your dns. First record you need to add is `A record` and another record is called `CNAME` record. A record is for mapping your domain name to IP address and CNAME record is used to map domain name to domain name. I have already changed the value for `A record` to my desired IP using this dashboard as shown in the above image in this site we use `CNAME` record to map `www.botsworld.me` to `botsworld.me` because they are same thing. There might be questions like is `www.botsworld.me` different from `botsworld.me`. The answer is yes, but after adding this `CNAME` entry thery will behave as same thing. why are `www.botsworld.me` and `botsworld.me` different thing? this is out of scope for this course, you can try to google it yourself.
I have similar record for `locus.com.np` i added `A record` and `CNAME` record in similar way to point to the ip `20.84.44.131` and hence we can use url like this in our browser
![Pasted image 20220708225827.png](/attachments/Pasted%20image%2020220708225827.png)

Now we can stop the running django server, then again start the server but this time we run it on the different port. This time we run django server on port `80` using command `python manage.py runserver 0.0.0.0:80` since port `80` is the default port for http, we can omit the port part from the url and we can still get the same result

![Pasted image 20220708230129.png](/attachments/Pasted%20image%2020220708230129.png)

### Using Nginx And Gunicorn

Now that every thing is going well there is one last thing we need to configure. when we start the django server with `python manage.py runserver` the started server is called development server, it is called development server because its just for development, it is only suitable for single or couple of users. it cannot handle requests from thousands of user, so we need separate software which can handle many users and also implement correct security policies. `Nginx` is the example of such high performance web server. Now we need to install `nginx` software and configure it to receive all request coming to port `80` and then foreward this request to django server which will be running locally in some port.
but django and `nginx` cannot directly communicate with each other so we need another software called `gunicorn` to facilitate communication between nginx and django. Gunicorm implements WSGI interface . WSGI is the specification which defines how web server should communicate with python web application frameworks like django.

so our new workflow to setup our web server is to

1. install nginx and gunicorn in our virtual machine
   To install nginx, copy the following script to the remote host, save it in a file named `install.sh` and use `chmod +x install.sh` to make this file executable and then run this script using `./install.sh` it will start downloading and installing `nginx` packaage

   `install.sh`

   ```sh

   	sudo apt install curl gnupg2 ca-certificates lsb-release ubuntu-keyring

   	curl https://nginx.org/keys/nginx_signing.key | gpg --dearmor \
   		| sudo tee /usr/share/keyrings/nginx-archive-keyring.gpg >/dev/null

   	gpg --dry-run --quiet --import --import-options import-show /usr/share/keyrings/nginx-archive-keyring.gpg

   	echo "deb [signed-by=/usr/share/keyrings/nginx-archive-keyring.gpg] \
   	http://nginx.org/packages/ubuntu `lsb_release -cs` nginx" \
   		| sudo tee /etc/apt/sources.list.d/nginx.list

   	echo "deb [signed-by=/usr/share/keyrings/nginx-archive-keyring.gpg] \
   	http://nginx.org/packages/mainline/ubuntu `lsb_release -cs` nginx" \
   		| sudo tee /etc/apt/sources.list.d/nginx.list

   	echo -e "Package: *\nPin: origin nginx.org\nPin: release o=nginx\nPin-Priority: 900\n" \
   		| sudo tee /etc/apt/preferences.d/99nginx

   	sudo apt update
   	sudo apt install nginx
   ```

1. start our django server not by `python manage.py runserver` but using command `gunicorn myproject.wsgi:application --bind 127.0.0.1:8000`. this command starts gunicorn server at IP address `127.0.0.1` and port `8000` here `127.0.0.1` is also special IP address which denotes current pc also called `localhost`.
1. Configure nginx to start listen at port 80 and forewared all the request to `localhost:8000`, configuration file looks something like shown below.
1. we need to copy this nginx configuration file to `/etc/nginx/conf.d/default` and reload the nginx server using `nginx -s reload` command

```
server {
	listen 80;
	location / {
		proxy_pass http://localhost:8000;
	}
	location /static/ {
		alias /var/www/static/;
	}
}
```

This server block has one `listen` directive and two `location` directive, listen directive is used to configure port where nginx server listens. in the above example nginx server be listening on port `80`. First location block block tells that for every request forward it to `localhost:8000` and second location block specify that if any paths has `/static/` in it then the static(files) content is from /var/www/static is delivered. for example if we request `locus.com.np/static/index.css` in the browser the request is not forwarded to django instead this static file is directly served by nignx. Our django project might geneerate static files like `css`, `images`, we can use `python manage.py collectstatic` commnad to collect these static files at once place and then use nginx directly to server these static content because nginx is very fast and optimized to serve such static files.

> written by Aayush Neupane
