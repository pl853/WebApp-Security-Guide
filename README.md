# Web Application Security Guide

Web Applications are currently the predominant source of software vulnerabilities exploited in online attacks.Quantity and importance of data entrusted to web applications is growing, and defenders need to learn how to secure them. Traditional network defences, such as firewalls, fail to secure web applications. There is a growing need and demand for web programmers to be security literate. </br>

In this guide you will learn to understand potential risks when creating a web apllication. You will also be able to reconize vulnerabilities and in that way learn how to defend your own applications from those vurnerabilities. In this guide the following subjects will be discussed: </br>
- Understand common mistakes of coders and vulnerabilities of web applications.
- Understand web application security and its importance.
- Explains how code developers’ mistakes may be exploited to the benefit of the attackers and how to prevent these attacks.
- Build secure web applications using secure coding practices.
- HTTP
- GET/POST REQUESTS
- GET REQUESTS
- POST REQUESTS
- SECURITY CONCERNS : GET/POST REQUESTS
- REFERER HEADER
- SECURITY CONCERNS : REFERER HEADER
- CACHING
- SECURITY CONCERNS : CACHING
- COOKIES
- SECURITY CONCERN: COOKIES
- SESSIONS
- SESSION HIJACKING
- PREVENT SESSION HIJACKING
- HTTPS
- PACKET SNIFFING
- PREVENT PACKET SNIFFING
- MITM (MAN IN THE MIDDLE ATTACK)
- PREVENT MITM ATTACKS
- CBM (CERTIFICATE BASES MUTUAL) AUTHENTICATION
- SECURITY LAB 1
- PASSING DATA IN SUBSYSTEMS
- INTRODUCTION 
- METACHARACTERS
- SECURITY CONCERNS: PASSING DATA IN SUBSYSTEMS
- SQL INJECTIONS
- PREVENT SQL INJECTION
- SHELL COMMAND INJECTIONS
- PREVENT SQL INJECTIONS
- USER INPUT
- INTRODUCTION
- INPUT
- SECURITY CONCERNS: INPUT
- VALIDATING INPUT

Tools used in this guide </br>
- VirtualBox, This tool is used to setup a secure test inveronment
- Postman, This tool is used for performing intergration testing with your API.

There are three specifications that are central to the web:</br>
- URL (Uniform Recourse Locators)
- HTML (HyperText Markup Language)
- HTTP (HyperText Tranfer Protocol)
 

## HTTP</br>
In the image below you can see a represantation of how you computer connects to a server.</br>
![client-server](https://user-images.githubusercontent.com/24454699/56094773-b2a16280-5ec5-11e9-8373-ca946d15258f.png)
</br>
A TCP connection is created, then the browser sends a HTTP request to the server asking for the wanted document. The webserver than replies with the page content and the closes the TCP connection again.

The browser is always the initiating party and the server nervel calls back. This means that HTTP is a client/server protocol. The client in this case doesn't always have to be a browser. It can also be your typical instagram application.

The HTTP is line oriented which means that the communication takes place using strings of characters which are separated by carriage return (ASCII 13) and line feded (ASCII 10).

## GET/POST REQUESTS 
There are 2 different types of requests that can be send by the client.
### GET REQUESTS
  In this request the client asks for information. With the GET request the browser is free to resent the request, for example, this happends when the user presses the back button on a website. (this is not suitable with for example, money transfers because this will resend the transfer each time the back button is pressed) In a GET request the parameters of the request are encoded in the URL. In the image below you can find an example of the GET request. </br>

  ![get_req](https://user-images.githubusercontent.com/24454699/56095124-1ed19580-5ec9-11e9-9224-5692be6ffa91.png)
</br>

  The following can be said about this image: 
  - The first line shows the Request-line. In the request-lin the GET is called the method token. The HTTP is the request URI and the 1.0 is the HTTP-version identifier.
  - The lines below the request-line are the Request-header lines.
  
  After the GET request is send by the client the server will send back a responce. (see image below)</br>
  ![responce_get](https://user-images.githubusercontent.com/24454699/56095184-b800ac00-5ec9-11e9-91e1-076b6c2b2eb6.png)
  </br>

  The following can be said about the image above:
  - The first line is called the status line. The HTTP/1.1 is called the HTTP-version, the 200 OK is called the status code. In this case the status code is 200 which means the request is OK. Another status code which we all reconize is status code 404 NOT FOUND which means that the requested webpage is not found.
  - The lines after the status lines (encirkeld in red) are calle the Request-header lines. In these lines you can find the content length. The value (in this case 84) represents the amount of bytes that are in the requested content.
  - The lines below that (encirkeld in blue) is the content that is requested. This is written in HTML.

### POST  REQUESTS
In this request the clients sends information that changes the information currently on the server. This request cannot be resend by the client without it asking permission for it.  The parameters of a POST request are hidden.  In the image below you can find an example of a POST request. </br>
![post_req](https://user-images.githubusercontent.com/24454699/56095517-5fcba900-5ecd-11e9-8fe6-4c2608f5174f.png)
</br>

It's basicly the same as a GET request only in this case the method token is POST. You can also see that the content-type is an encoded form. The content-lenght is again the amoubtn of bytes posted by the request. In this case a user tries to login using the username jdoe and the password BritneySpears. This can be seen in the last line.</br>

URL encoding means that you change certain characters found in the URL by encoding them using a % sign followed by tho hexadecimal digits. (see image below)</br>

![encoded](https://user-images.githubusercontent.com/24454699/56095603-0617ae80-5ece-11e9-8e11-f91f98a9946d.png)
</br>

### SECURITY CONCERNS: GET/POST REQUESTS
The origin of all the requests are on the side of the client. This means that an attacker can replace the client (EX. a browser) with something completely different. For example a proxy can be used to manipulate the data sent to the server. They sit between your client (ex. your browser ) and the server. The proxy lets the attacker change the header and data before passing it to the server.</br>
A situation where this could be usefull for an attacker: </br>
A user want so send money via a bank transfer. The user wants to send the money to an account with the number 1234. The attacker changes this account number to his own account number, 4321. When the user presses send  the money will be send to account 4321 instead of account 1234.  

## REFERER HEADER 
On a request the referer header contains the url  of the website  where the document is located. This is also the case when you have an image on your website that is from another website. (in the image below you can see an example of this) </br>
![urlheader](https://user-images.githubusercontent.com/24454699/56095993-ebdfcf80-5ed1-11e9-942d-b6e8ec2b6705.png)
</br>
In the image above the the image used is from the website : http://www.site.example/index.html. This meanse that you use a snippit (small part) of the html code from that website. It's the same for the link below the image. 

### SECURITY CONCERN: REFERER HEADER
Because a part of the code,  from the website that has the image on it,  is used in your own website, it will  also use any JavaApplets, ActiveX scripts and plug-ins included in that  page.

## CACHING
The term Caching refers to temporarily storing documents on the client or server side to reduce the download time. When we talk about caching you can devide it in two types of chaches:
- Local cache </br>
  This is manged by the client (your browser). When the client sends a request for a type of document it saves the document on your disk. When you go to the document (the page in this case) again the loading time will be much lower because it can get the document from your local storage instead of a remote server.
- Shared cache </br>
   This cache is typically a server in the local network. If one user reads an online newspaper, and another user tries to access the same newspaper the second user will get a local copy because it was already requested by the first user.  </br>

   The image below shows the 2 types of caches: </br>

![clientservercache](https://user-images.githubusercontent.com/24454699/56096371-c30e0900-5ed6-11e9-87aa-d1db6e25261c.png)
</br>

### SECURITY CONCERN: CACHING
Some documents should not be cached. A few examples of those documents are:
- The stock information on a webstore. The user should always be served up to date stock information. If the information from the day before is cached and then retrieved by an user there is a possiblity the user recieves out of date stock information.
- Another situation could be in an internet cafe. If user 1 has send information on a banking website and leaves, then user 2 goes to the computer that was just used by user 1 and then presses the backbutton, user 2 will be able to retrieve the banking info of user .

The sites need a way to tell the browser and proxies to not save these kind of documents. This is done in the HTTP headers. Different versions of HTTP apply different mechanisms for cache control. This means that an older version of HTTP could also be a security consern.

## COOKIES
HTTP is a stateless protocol. This means that there are no connections to previous request made by the same client. To create a connection (state) between these requests we make use of cookies. Cookies are an extension of HTTP to give us just the state, So with cookies the webserver asks the client to remember a small piece of information. This info is passed back by the client on each request to the same server.</br>

An example of a cookie is: On google search the user can set the amount of results returned by a google search. The cookie makes sure the amount set by the user is remember each time the user does a search on google.</br>

The HTTP header is used for both setting and returning the cookies. When the server want the client to remember a cookie it passes a Set-Cookie Header in the response. The image below is an example of a Set-Cookie Header. </br>

![set_cookie_header](https://user-images.githubusercontent.com/24454699/56096540-14b79300-5ed9-11e9-8a07-1c79ca99142e.png)
</br>

The cookie is then returned using something called the cookie header. (see image below)</br>

![cookieheader](https://user-images.githubusercontent.com/24454699/56096566-7415a300-5ed9-11e9-8cfd-22d7d749cfac.png)
</br>

### SECURITY CONCERN: COOKIES
Using cookies comes in very handy. There are some security concerns it brings with them. The concerns are as follows:
- Cookies may be limited in size, this means that space consuming states cannot be safely represented using cookies.
- Cookies are handled on the client-side, as we know right know client-side stuff can be manipulated by users with bad intentions. 

Solving these concerns can be done by storing the cookie information on the server side.

## SESSIONS
Session are a collection of variables that make up a state. They are located on the server-side. To make sure the session is associated with the correct client a session ID is passed on each request to the server. So the session ID uniquely identifies with one session object on the server. </br>
The image below shows a visual represantation of a session object. </br>

![SessionID](https://user-images.githubusercontent.com/24454699/56096940-cb1d7700-5edd-11e9-927f-71faa21290d6.png)
</br>

### SESSION HIJACKING
These days a lot of websites use session based login. This means a session is initiated when the user has given a valid username and password. But what if someone gets access to the session ID of the user thats logged in? </br>
In this case the attacker would not need the password of the victim since the session ID works as a temporarily replacement for the password.  There are multiple ways an attacker can get access of the SessionID :
- Guess it
- Calculate it
- Brute-force it
- Trial and error search
- Cross site scripting
- Use referer header
- Packet sniffing
The list goes on and on

### PREVENT SESSION HIJACKING
As mentioned above there are a lot of ways an attacker can find the sessionID. To prevent this from happening you need to improve the secrecy of the SessionID. The key to preventing your sessionID from being stolen is making it unavailable to third parties. A lot of websites use secondary measures to prevent session hijacking even after the sessionID is compromised.</br>
CAUTION : none of these secondary measures offer full protection to session hijacking, the secrecy of the sessionID is the only real mechanism for protection.

### SECONDARY MEASURES FOR PREVENTING SESSION HIJACKING
There are multiple secondary measures that can be taken to prevent session hijacking:
- Tie the sessionID to the IP address of the client. </br>
  This measure wont protect you from attackers that use the same IP address. For example when using a VPN you have the same IP addres as other users that use the same VPN.
- Tie the sessionID to certain HTTP Headers passed by the client.  </br>
   This is also not bullet proof since the attacker can replicate the HTTP headers your client sends.
- Have variable sessionID's </br>
   If you make sure the sessionID changes with every request made by the client it's harder for the attacker to hijack the session. Unfortunatly this is also not secure enough since it can take a while for a user to send a new request. In the time before a new request an attacker could have already taken over the whole session blocking the victim of further access.

 ![sessionwarning](https://user-images.githubusercontent.com/24454699/56097146-1e90c480-5ee0-11e9-9abf-e955eb4f09b4.png)
   </br>

## HTTPS
In the procces of making a web server secure, encryption plays an important role. In a web setting, encryption usually means HTTPS.  This means that all the HTTP  communication is done over an encrypted channel. To check if a webserver usses encryption you can either:
- Check the url. If we take githubs website for example you will see that the url looks like this :  https://github.com/PieterLems/.  As you can see, in front of the github.com there is HTTPS, which meanse the webserver usses encryption.
- Another way to check this, is to check the logo in front of your URL bar of your browser. As you can see in the image there is a shield in front of the URL bar. This means that the webserver usses encryption.

  ![githubsecure](https://user-images.githubusercontent.com/24454699/56097236-1be29f00-5ee1-11e9-8163-fc7901236364.png)
</br>

The encrypted channel can be provided by the following protocols:
- Secure Socket Layer (SSL)
- Transport Layer Security (TLS)

CAUTION: The encryption protocols only protect the connection between the client and server. The attacker can still attack both the client and the server, but he will have a hard time attaking the communication between those two. </br>
The image below is a visual represantation of the difference between a HTTP (on top of the image) and a HTTPS (at the bottom of the image) connection.

![secureinconnection](https://user-images.githubusercontent.com/24454699/56097339-36694800-5ee2-11e9-96c4-7ad2aa4ddd8d.png)
</br>

### PACKET SNIFFING
Packet sniffing is a way to attach the networking transport rather than the client. First you need to understand what a packet is. A packet is a unit of data made into a single package that travels along a given network path. Data packets are used in Internet Protocol (IP) transmissions for data that navigates the Web, and in other kinds of networks. </br>
The image below shows a visual represantation of an attacker sniffing packets transfered by the victim.

![packetsnif](https://user-images.githubusercontent.com/24454699/56097386-d030f500-5ee2-11e9-89be-a0202b1e4bba.png)
</br>

### PREVENT PACKET SNIFFING
To prevent data being stolen when your packets are being sniffed you should make use of encrypted connections (HTTPS).  This won't prevent the attacker from sniffing your packets but all the content of the sniffed packets are random strings of data.</br>
A visual represantation of what happends when packets are being sniffed over an insecure (at the top of the image) and  a secure (at the bottom of the image) connection is shown in the image below.

![securesnif](https://user-images.githubusercontent.com/24454699/56097452-be038680-5ee3-11e9-8158-87e723a7fc4d.png)
</br>

### MITM (MAN IN THE MIDDLE ATTACK)
In a MITM attack the attacker tricks the victim's computer into connection to the computer of the attacker rather than connecting it to the real server.</br>
Take for example a situation where a user connects to a bank server:
- The attacker tricks the user's computer in thinking that the attackers computer is the bank's server.
- The attacker than forwards all the communication to the banks server. 
- From the victim's point it looks like he's connected to the bank server but in reality all the communication is send trought the attackers computer.
- This enables the attacker to intercept, read and modify all the communication made between the 2 parties. (bank and victim)

A visual represantation of a MITM attack is shown in the image below:

![mitm](https://user-images.githubusercontent.com/24454699/56097508-bb556100-5ee4-11e9-8524-a7bdd3e27197.png)
</br>

### PREVENT MITM ATTACKS / CBM (CERTIFICATE BASES MUTUAL) AUTHENTICATION
When you make use of a HTTPS connecting the client always verifies something called the server's certificate. This certificate is an unique identifier of the webserver. </br>
The image below shows a certificate</br>

![certificate](https://user-images.githubusercontent.com/24454699/56097648-cf01c700-5ee6-11e9-867d-5a570fc18c93.png)
</br>

The image below is a visual represantation of how the servers certificate is verified. <br>

![certificateverify](https://user-images.githubusercontent.com/24454699/56097685-551e0d80-5ee7-11e9-9951-498b35ffba70.png)
</br>

HTTPS doesn't always prevent the attacker from succeding when performing a MITM attack, this can be caused by a few factors:
- Ignorant users, the user neglects the warnings given by the browser.
- The browser doenst give out any warnings.
- The user falls for cheap domain name or protocol tricks used by the attacker. 
- Fake websites with similar domains. (the html of a website can be easily replicated by the attacker and the domain name can be spoofed in something that looks like the domain the victim tries to access)
- Certification authorities mistakes, the CA may be tricked into giving out false certificates.
- The browser trusts a CA (certificate authoritie) that isn't trusted by the user.
- Bugs in the browser, the browser has a buggy SSL/TLS implentation.
- The user's computer is compromised by the attacker.

## SECURITY LAB 1

## PASSING DATA IN SUBSYSTEMS
When using dynamic webapplications data is passed to one ore more subsystems. A few examples of this subsystems are:
- SQL databases
- Operating Systems
- Libraries
- Shell command interpreters
- Xpath handlers
- XML documents
- Legacy Systems
- User's browser

The way the communication between the application and the subsystems takes place is by building strings containing control information and data. But what data is passed?
The subsystems contain parser which decode incoming strings character by character, and then decides what to do based on what they read. The strings could represent names, addresses, passwords, webpage's ... just about everything. </br>
A visual representation of this can be found in the image below. </br>

![commsub](https://user-images.githubusercontent.com/24454699/56097894-a5966a80-5ee9-11e9-8a00-488f899f5193.png)
</br>

### METACHARACTERS
When we use special characters as input those characters won't be treated the same. There is a possiblity the system reads this character as a metacharachter. </br>
These characters won't always be treated asa plain text. They can become control characters. metacharachters are not a threat by themselves. </br>

### SECURITY CONCERNS: PASSING DATA IN SUBSYSTEMS
They become a threat when developers think they are passing them as pure data but that data makes the subsystem do something unexpected.</br>
If the subsystem reads a metacharachter it may stop reading pure data and start reading commands entered by the attacker.

## SQL INJECTIONS
One of these attacks where an attacker makes use of metacharachters is called a sql injection. We all know the syntax of SQL and we also know that metacharachters are involved in writing queries. </br>
In SQL Injections,an attacker is able to modify or add queries that are sent to a database by playing with input to the webapplication. The attack works when a program builds queries based on strings from the client, and passes them to the database server without handling characters that have special meaning to the server / subsystem. </br>
In the image below you can find a visual represantation of a SQL injection. </br>

![sqlinj](https://user-images.githubusercontent.com/24454699/56126074-dc13ca00-5f69-11e9-8437-49b43692d776.png)
</br>

Below we will describe an example of a sql injection</br>
In this example we will use a situation where a user want to register to a website that uses a SQL database as backend. The java code in the application is as follows: </br>

![sqlinjec1](https://user-images.githubusercontent.com/24454699/56126291-5b090280-5f6a-11e9-87fe-4553300e230c.png)
</br>

Then there are 2 uses that want to register. The first user is : </br>

![sql1](https://user-images.githubusercontent.com/24454699/56126343-7d028500-5f6a-11e9-9c20-8fb914c8124b.png)
</br>

And the second user : </br>

![sql2](https://user-images.githubusercontent.com/24454699/56126413-a8856f80-5f6a-11e9-89c6-ca793f076210.png)
</br>

In the picture above the character encirkeld in red is the metacharachter that makes the system do something unexpected. Take for example a login form in a web application which uses the following code to check the input credentials. (image below) </br>

![sqlattack](https://user-images.githubusercontent.com/24454699/56126784-39f4e180-5f6b-11e9-9933-e6ba9b639a0c.png)
</br>

If the attacker happends to know that there is a user named john', he fills in john' as user name. This will cause the system to fill in the sql query as follows : </br>


![sqlattack2](https://user-images.githubusercontent.com/24454699/56126894-8809e500-5f6b-11e9-83d3-63b47177ec12.png)
</br>

Now the attacker is logged in as user john' without needing his password. The reason for this is because the metacharachter (' in this case), disables the test for matching the password.
### PREVENT SQL INJECTION
So what is the problem in the example above? The problem is not the metacharachter, its all about contexts and parsing. In the image below everthing is OK up to the first singel quote, because it switches to parsing a string constant. </br>

![stringconstant](https://user-images.githubusercontent.com/24454699/56128398-061bbb00-5f6f-11e9-8e18-06f3a34fdcd2.png)
</br>

The real problem is: The attacker is allowed to make the SQL parser switch context. (reading plain text to inserting queries).

To solution 
## SHELL COMMAND INJECTIONS

### PREVENT SHELL COMMAND INJECTIONS

## USER INPUT

### INTRODUCTION

## INPUT

### SECURITY CONCERNS: INPUT

## VALIDATING INPUT