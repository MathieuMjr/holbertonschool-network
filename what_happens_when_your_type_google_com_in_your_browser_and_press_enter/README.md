This week at Holberton School, we have spent the week learning what the mechanisms are behind the Internet, from the address you type into your browser to the website displaying on your screen.  

Today, I invite you behind the curtain to discover together how it works; I'll talk to you about some familiar notions you might already have heard of, like **IP addresses** or even **DNS** (if you have unfortunately experienced connection issues with some websites).


## Some notions first :

**Internet:** is the worldwide network connecting networks together. Physically, it is mostly terrestrial and submarine cables connecting networks of computers and servers together (ok, it is also Wi-Fi waves at your place).

**IP:** IP addresses are just **like your postal addresses** but for your computer. When you are at home, you have a private IP address on the local network connecting you with other computers or printers, for example. On the net, you have a public IP address.  
It looks like this: 8.8.8.8 – four numbers separated with dots. Since 2017, a new format of IPs has been introduced, because **4 billion of these addresses are no longer enough to connect the world to the Internet**.

**Servers:** well, they are computers too, hosting websites, data, and services, bunched in buildings all around the world, running 24/7 and waiting and listening for users’ requests...  

With those first requirements, we can now dive into the web... and try to visit google.com – sorry for the lack of ambition.


## Google.com means nothing to a network

**Google.com is a domain name**; the Internet does not know what to do with this. 

What **the network needs is the IP address of the server hosting Google’s website...**


In the very beginning of the net, you would have to memorize each IP address if you wanted to visit a website. 

Luckily, we now have the DNS system: Domain Name System. You only need to memorize a domain name; **the DNS finds the IP address for you.**

---

## The journey to the IP begins:

You type google.com, and press Enter.

First, your browser checks its cache and your OS cache: maybe you’ve visited it lately ?

Let's say you have not: your computer will send a request to **the DNS resolver** – some mysterious device somewhere provided by your Internet provider.

You're unlucky again... the DNS checks its cache in case it has saved the IP from a previous request, but no one on the network your DNS resolver knows has visited google.com lately...

The DNS resolver asks a server named **"root server"**. This server doesn’t know the IP address of google.com, but it checks for the end of your domain name, the .com, .org, etc.  
**The root server then gives the IP address of a TLD server in charge of the .com domains.**

The DNS goes to the IP address the root server gave it and requests the TLD server. The TLD server does not know the IP either, but it knows **the address of the "authoritative server"**.

The DNS resolver finally requests **the authoritative server**; this server **stores an "A record," a record matching the domain name with the IP.**

At last, the DNS server can send you back the IP address you were looking for! It was long, isn’t it?<br>**Well, it was only 80 ms**.

Your browser and your OS keep the IP address in cache memory so it can find it faster next time... 

But they won't keep it for ages: what if the IP changes and the one you stored is no longer valid? That is why, with the IP, comes a TTL: "time to live," indicating how long the IP is kept in cache memory.

---

## Connecting to Google!

The browser can finally send a request to the right IP address, right to the server hosting Google.com!

It reaches the IP and establishes a **TCP connection**: a special kind of connection where it **makes sure no data is lost during communication**.

Then the **connection is secured** with the **SSL or TLS protocol**: data is **encrypted**, and only the browser and the server it is connected to know how to read it.  
To know what requests are made, what data is sent, the HTTP protocol is used, following rules to tell if it is a request or a response, for example. Phew.

Did I say your browser reached the google.com server? Well, not in the way you might think... **it reached a "proxy".**

---

## In the restaurant's kitchen:

This proxy server **hides another network of servers with several components of the Google application, and many instances of Google applications running!**  
This is a key step where the traffic is balanced between several Google applications so it can respond quickly.  

Let's take a moment now to see **what a website is made of and how it is served**.

On the physical servers, there are **some other kinds of server**s... They are **software** running on the machine, **serving files or data**.  
Think of it as the server at the restaurant: your browser asks for a meal, and the server goes back into the kitchen and comes back with what the browser needs.  
You can't know by yourself how it is made inside the kitchen, nor where to find what you are looking for.

For a typical large-scale website, you have:  
- **A web server**: its job is to deliver to your browser the **files building the website interface** on your screen.  
- **An application server**: its job is to **ask the program to create or retrieve some data** you requested.  
- A **database** **storing** the data you created **or retrieving data** you requested.

Those are very sensitive parts of a website...  
That is why, between you and the proxy, between the proxy and the servers hosting web and application servers, and between the database and the application servers, there are **firewalls**.  
They are software or physical devices in charge of the security policy and communications authorizations, checking requests, IPs, ports.

---

## Data flow through the connection:

Now, let's go back to our connection with the proxy. 

The proxy sends your request to another physical server hosting a web server.

The web server sends code so your browser can display the website interface on your screen.

Then you type a search. The search is sent through the network to the proxy.  

The proxy chooses a web server to send the request.  
The web server sees data from the database is requested – it sends the request to the application server.

The application server uses a program to build a request and query the database.

The database builds a list of results and sends it back... and the result goes back through the application server, then back to the web server, to the proxy, and finally to your browser!  

That's it: you have your Google search results :)