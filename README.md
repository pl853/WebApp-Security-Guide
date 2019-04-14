# Web Application Security Guide

Web Applications are currently the predominant source of software vulnerabilities exploited in online attacks.Quantity and importance of data entrusted to web applications is growing, and defenders need to learn how to secure them. Traditional network defences, such as firewalls, fail to secure web applications. There is a growing need and demand for web programmers to be security literate. </br>

In this guide you will learn to understand potential risks when creating a web apllication. You will also be able to reconize vulnerabilities and in that way learn how to defend your own applications from those vurnerabilities. In this guide the following subjects will be discussed: </br>
- Understand common mistakes of coders and vulnerabilities of web applications.
- Understand web application security and its importance.
- Explains how code developers’ mistakes may be exploited to the benefit of the attackers and how to prevent these attacks.
- Build secure web applications using secure coding practices.

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
- GET </br>
  In this request the client asks for information. With the GET request the browser is free to resent the request, for example, this happends when the user presses the back button on a website. (this is not suitable with for example, money transfers because this will resend the transfer each time the back button is pressed) In a GET request the parrameters of the request are encoded in the URL. In the image below you can find an example of the GET request. </br>

  ![get_req](https://user-images.githubusercontent.com/24454699/56095124-1ed19580-5ec9-11e9-9224-5692be6ffa91.png)
</br>
  The following can be said about this image: </br>
  - The first line shows the Request-line. In the request-lin the GET is called the method token. The HTTP is the request URI and the 1.0 is the HTTP-version identifier.
  - The lines below the request-line are the Request-header lines.
  
  After the GET request is send by the client the server will send back a responce. (see image below)</br>
  ![responce_get](https://user-images.githubusercontent.com/24454699/56095184-b800ac00-5ec9-11e9-91e1-076b6c2b2eb6.png)
  </br>

  The following can be said about the image above:
  - The first line is called the status line. The HTTP/1.1 is called the HTTP-version, the 200 OK is called the status code. In this case the status code is 200 which means the request is OK. Another status code which we all reconize is status code 404 NOT FOUND which means that the requested webpage is not found.
  - The lines after the status lines (encirkeld in red) are calle the Request-header lines. In these lines you can find the content length. The value (in this case 84) represents the amount of bytes that are in the requested content.
  - The lines below that (encirkeld in blue) is the content that is requested. This is written in HTML.

- POST


