---
author: "Minh T. Nguyen"
title: "Understand Web Development"
date: "2023-02-02"
description: "Virginia Tech's Web Development course note."
tags: ["web development", "vue.js", "mysql", "java", "html / css", "figma", "long-read"]
categories: ["software engineer"]
series: ["Software Engineering"]
aliases: ["migrate-from-jekyl"]
ShowToc: true
TocOpen: false
draft: false
weight: 5
---

<p style="color: #286EE0"><strong>Status:</strong> [Latest]</p>

**Course Description:** Web application with Topics regarding Networking, Security, Encryption, Database concepts, Distributed Computing models. After completion, student should knows about the e-commerce technology
- Data centric web app: authentication, authorization, session handling, resource management, user history.
- Recognize fundamental internet and web protocols such as TCP, UDP, HTTP (including GET and POST) requests and identify the characteristics of ech
- Identify key features of client-side web technology: HTML, CSS, Javascript and use them to implemnt a basic web application design
- Identify key features of server-side web technology such as REST APIs and the DAO patterns, and use them in an application to create dynamically-generated web content.
- Discuss application security issues related to web-based, systems, including authentication, authorization, confidentiality, and adata integrity.

**Note**: later add the quiz session of midterm, final, and assignment to text. Create a repo to post the project every week!

## Week 1: Application Design
### [Inter-Networking](https://www.youtube.com/watch?v=y_i9zTKRbVQ&list=PLRjaigwVuv548GJeJR5MvTqhKOTaolL_p&ab_channel=Dr_K)

**Circuit Packet Switching**
- Circuit Switch Network vs Packet Switch Network:
  - Circuit Switch
    - Original phone system had a purely circuit switched foundation. 
    - All information within a call takes exactly the same fixed path.
    - Routing only occurs before the call.
  - Packet Switch
    - The Internet protocol (IP) provides a decentralized packet-switched foundation.
    - Each packet is individually and continuously routed, based on its destination address.
- Packets may arrive out of order. A packet may be dropped or lost. A packet may be duplcated.

**TCP-UDP**
- TCP == Transmission Control Protocol. This is a connection-oriented protocal favors reliability over speed. This is the most compliment to the internet protocol. First, you will establish connection between two devices, which is called a handshake. This protocol make sure that you get all the info intact. Due to its speed and reliable, TCP is most common to be paired with IP
- UDP == Universal Datagram Protocal: This is a connection-less protocal (without handshake), the package is just streaming without caring the other device turn on or not. UDP is great for live streaming videos (fast over perfect, the packet lost just make it lag).
- Examples:
  - Amazon uses TCP as we want payment reliability
  - Dropbox uses TCP as we trust Dropbox maintain the sent document intact
  - DNS Lookup (has a domain name and want to get IP address) use a packet of info to check UDP.
  - Facebook uses TCP to make sure the info is sent correctly. 
  - Gmail uses TCP.
  - VOIP (voice of IP) uses UDP as we can ask people to repeat.
  - World of Warcraft uses UDP 
  - Netflix uses a combination between TCP and UDP.

**OSI Reference Model**
- Open Systems Interconnection (OSI) is an abstract model of networking which divide communication network into 7 layers. This is the most popular communication model that represent how communicate over the internet.
- OSI is a protocol reference models provide an abstract view of the network, and group functionality into layers. Each layer provide a service to the one above it and each has their own set of protocol to make sure the network will work.
- OSI has 7 layers:
  - 1st (Physical Layer): Deliver bits over physical link (or wireless). Worry about 1 bit to 1 place to another. Analog vs Digital vs Radio Signal?
  - 2nd (Data Link Layer): Groups bits into addressed frames for transmission over physical links (over local media network). Address for local machine only, not IP address. So that the bit can get 1 node to another within a local area network. We plug the cable to network hub and that hub tell the bit where to go within the local network. 
  - 3rd (Network Layer): Deliver packets with routing services across multiple data links. Connect data links (or local area network). This is where the internetworking happen. This is the internet layer where the internet protocal resides.
  - 4rd (Transport Layer): Deliver data from operating system to operating system, not just computer to computer. When the data get to OS, it should be ready to use. This is there the data is package together. This is where error checking occurs. This is where TCP and UP perform their function.
  - 5th (Session Layer): Manages connection between local and remote application. Concerns with sockets and ports in the machine.
  - 6th (Presentation Layer): Convert operating system standards to or from network representations. This is where encryption resides. This is how our application SEE the network
  - 7th (Application Layer): Ensure communication between distributed software components. This is where we develop our application.

**Distributed Computing Model**
- Client-Server Model: most common model. The server sits idle to the request. The client initiate the request. To first establish the connection, we use TCP (connection-oriented protocol). The client request a service and the server response to the request. The client-server model is call a 2-tier Model.
- 3-tier-model (MVC): Most common
  - Presentation tier: Front-end interface and send request to the client. The main function is to translate tasks annd results to something the user can undestand.
  - Logic tier: Handle the request, often that request involves in the data tier. The main function is to coordinate the applicaiton, processes commands, make logical decisions and evaluates, and performs calculations. It also moves and processes data between the two surrounded layers.
  - Data tier: information is store and retrieved. The information is then passed back to the logic tier for processing, and then eventually back to the user.
  - Note: The llogic tier can become complex and split into multiple tiers. We called it a multi-tier model.
- Peer-to-Peer Model: All the nodes shared resource to each other. Popular in Napstern MP3 file-share, here, every computer is a server and a client.

**Sockets Ports**
- A network socket is an endpoint of a connection across a computer network. An endpoint of a connection is not a device but an application in device. Socket not only include an IP address in a particular device, but also a particular port for a software application is listening, port 80 is default for web server. 
  - For example: When you type in domain name "nytime.com", a domain name server (DNS) translate it to an IP address (such as 8.8.8.8).
- An Internet Socket consists of:
  - A transport protocol (TCP, UDP, ...).
  - An IP address (IPv4 or IPv6).
  - A port (default for web servers is 80).
  ```python
  Socket socket = getSocket(type="TCP")
  connect(socket, address="8.8.8.8", port="80")
  send(socket, "Hello, world!")
  close(socket)
  ``` 
- A DNS (domain name server) translate a name server "nytime.com" to IP address (8.8.8.8).
  - IPv4: 32 bits with 2^32 unique addresses. This is not enough for the internet.
    - Each number is 8 bits so we have 4 number x 8 bits = 32 bits per address.
    - Ex: 8.8.8.8
  - IPv6: Add more internet addressing, use 128 bits addressing. (0-FFFF)
    - Each number is 8 bits so we have 16 number x 8 bits = 128 bits per address
    - Ex: 2001:4860:4860:8888

### W3 Roadmap Notes
- The distinction between front-end and back-end is fundamental to web development. Front-end development involves the code that is served to the client (a web browswer). Back-end development involves the code that is run on the server. Typically a database, code related to sharing the data and the business logic for the application.
- Learn the basic:
  - HTML: HTML + HTTP
  - CSS: CSS + Responsive Design
  - JS: JS + ES5 + ES6
  - Note: ES5 is a Javascript specification. Almost all browswers are ES5 compliant, but most modern browsers are also ES6 compliant.
- Dig Deeper:
  - HTML: HTML DOM, XMLHttpRequest (XHR). 
  - CSS: CSS Icons, Google Fonts.
  - JS: XML, JSON, AJAX, Fetch API
  - Note: XHR is supported in almost every browswer. AJAX uses the XHR so clients can access and update data on the server without having to refresh the page. Fetch is slowly replacing AJAX/SHR. It does everything they can do, it's easier to use and it works well with web services.
- What is [AJAX](https://www.youtube.com/watch?v=3l13qGLTgNw&ab_channel=WebConcepts) (Asynchronous Javascript and XML)? A Web Dev technique to send and retrieve data in the background without having to refresh the page.
  - Every second that the Twitter web makes a request to its server to check if there is any updates or tweet. So, instead of sending new request through HTTP URL bar, AJAX us Javascript XMLHttpRequest object to make http request behind the scene.
- Choose Tech/Framework:
  - CSS: Grids, Flexbox, Bootstrap
  - JS: jQuery, Angular, React, Vue.js
  - Note: Boostrap is the main CSS frameworks. Grids and flexbox are important layout technologies that can be use with/without Bootstrap

### Additional Resources
- [The Non-Designer's Design Book](): Read Chapter 1-5.
- [Designing for accessibility]()
- [W3Schools Web Development Roadmap]()
- [W3Schools HTML5 Tutorial]()

### Codebase

## Week 2: Design in HTML & CSS
### [HTTP](https://www.youtube.com/watch?v=n_FWZii9D-Q&list=PLRjaigwVuv55p6POy8pH2hdlswenFfoNT&ab_channel=Dr_K)
**HTTP, Servlets, and JSP**
- Website is a static page with HTML + CSS that connect to the internet.
- Native GUI Application is an application that run locally in your machine. But the user have to download the application while keep it update. Usually it is written in Java.
- Best of both world: Dynamic Web Application: Run on the web while update.
- Web Client vs Web Server:
  - Client allows the user to request resources from the web server and display the result of that request. The client use the web browser and the browswer knows how to communicate with the server and the browswer knows how to interpret HTML code and it render the webpage recieved by the server.
  - Server recieves request from client, allocate the resource and send back to client.
- HTML vs HTTP:
  - HTML (Hypertext Markup Language): The server typically sends the browser instructions written in HTML. This tells the browser how to display the requested content to the user
  - HTTP (Hypertext Transfer Protocol): The protocol used by clients and servers to communicate with one another. It handles the simple request and response conversations.

**Request Response**
- HTTP Protocol is the request-response protocol for the web.
- Key elements of the HTTP request stream:
  - HTTP methods (action to be performed)
  - The page to access (a URL).
  - Form parameters (like arguments to a method)
- Key elements of the HTTP response stream:
  - A status code (for whether the request was successful)
  - Content-type (text, picture, HTML)
  - Content (actual HTML, image,...)
- There are 2 types of HTTP requests:
  - GET: The user click a link to a new page, then the browswer sends a GET request to the server, asking for the new page.
  - POST: The users fills out the form and hit the submit button, then the browswer sends a POST request to the server, giving the server the data from the form.
  - Note: You can send some data with a a get request. It appears after ? in the URL, the param is separate by &. However:
    - The total number of char you sent with GET is limted by the server.
    - The data you sent is appended to the URL in the address bard, so it will be expose.
  - For GET, the request belong to the request line (limited char) while POST stores the request to request body (payload).
- Other HTTP Request Methods:
  - HEAD: Same as GET but returns only HTTP Headers and no document body.
  - PUT: Uploads a representation of the specified URI.
  - DELETE: Deletes the specified resource.
  - OPTIONS: Returns the HTTP mehtods that the server supports.
  - CONNECT: Converts the request connection to the transparent TCP/IP tunnel.
- Status Code: Check Image
  - 200 == the request is OK for sucessful HTML.
  - 403 == the request is OK but the server refuse to response to it! Try to access forbidden directory.
  - 404 == page can't be found. But can reappear. Happen if we put wrong URL
  - 500 == internal server error. Some generic error in the server side but other message does not make sense!
- Cookie = small piece of data store in browser so the website know certain info about you!

**Dynamic Sites**
- URL (Uniform Resource Locator): Every resource in url has specific address.
  ```sh
  http://www.wickedlysmart.com:80/beeradvice/select/beer1.html
  ```
  - `http` is the protocol.
  - `www.wickedlysmart.com` is the unique name of server (mapped to unique IP address)
  - `80` is the default web server
  - `/beeradvice/select/` is the path to the resource.
  - `beer1.html` is name of the request content. 
- How does everything connect and work together?
  - 1. a user typpe URL to browswer.
  - 2. The browser sends a HTTP GET request.
  - 3. The GET request sent to the server.
  - 4. The server found the page identified in the URL.
  - 5. The server generate the HTTP response that include the page with 200 status code
  - 6. The HTTP response is sent to the browser
  - 7. The browser renders the HTML.

### Vue 3 Fundamentals
- Vue is a Javascript frameworkd that makes use of a multiple components to implement a Single-Page Application. Single-page application just have one HTML page (index.html). Vue uses JavaScript to modify that page so that it can look like any traditional web page in the application. 
- We use Vue for its reactivity property: There are 2 ways of data-binding. Let's say we have a string and print-out that string, we can bind (with directive v-model) the input tag with that string using v-model. When we change the input, the data will be changed (and synced).

### Additional Resources
- [Head-First Servlets and JSP]()
- [W3Schools HTML5]()
- [W3Schools CSS]()
- [A Complete Guide to Flexbox]()

### Codebase

## Week 3: Design in Vue.js

### Codebase

## Week 4: DAO Pattern & RestAPI
**Databases**
- Database proide structure of data, protect data from unauthorized access or changes.
- Relational databases: table of related data. "Relation" is a set of columns of related data.
- Foreign Key: A primary key in a table when it call from another table.
- Types of Database relationship:
  - One-to-many: For example, to map a CustomerID (first col) of a table to a (second col) of another table.
  - Many-to-many: For example, many order can include many dishes and many dishes can include many order. We can't use foreigh and primany key directly but we have to use a linking table
  - One-to-one: To associate 1 record from 1 table to another record in another table.

**DAO Patterns (implemented with JDBC)**
- Data Access Object Pattern: DAO is a popular design pattern to implement persistence layer of Java application. 
- DAO object is a way to represent the database as a Java class which provide a CRUD operations. 

**[DAO Find Methods](https://www.youtube.com/watch?v=Xj93xLTRqhg&ab_channel=Dr_K)**
- For product DAO, we can have
  - findAll() that return a list of model objects.
  - findByCategoryId()
  - findByProductId()

**REST APIs**


### Codebase

## Week 5: Fetch

### Codebase

## Week 6: State Management

### Codebase

## Week 7: Session Management

### Codebase

## Week 8: Client-Side Validation

### Codebase

## Week 9: Server-Side Validation

### Codebase

## Week 10: Transaction & Hardening

### Codebase

## Citation
Cited as:

<blockquote>
    <summary>Nguyen, Minh. (Feb 2023). Web Development Note.</summary>
    <summary>https://mnguyen0226.github.io/posts/webdev/post/.</summary>
</blockquote>

Or 

```sh
@article{nguyen2023mlsys,
  title   = "Web Development Note.",
  author  = "Nguyen, Minh",
  journal = "mnguyen0226.github.io",
  year    = "2023",
  month   = "February",
  url     = "https://mnguyen0226.github.io/posts/webdev/post/"
}
```

## Reference


<center>
    <img class="img_size" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/webdev/imgs/washingtondc.png" />
</center>
<figcaption class="img_footer">
    Fig. X. Sunday at Washington DC, U.S.A. (Image source: 
    <a href="https://unsplash.com/photos/fbtHV94f-bA" class="img_footer">Jorge Alcala @ Unsplash</a>).
</figcaption>

<!-- CSS Styling -->
<style>
.img_size {
  width: 100%;
}

.img_footer {
    color: #888888;
    text-align: center;
}
</style>
