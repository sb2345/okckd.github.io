---
layout: post
title: "[General] Application Server vs. Web Server"
comments: true
category: general
tags: [  ]
---

## Overview

A Web server __exclusively handles HTTP requests__, whereas an application server __serves business logic__ to application programs through any number of protocols. 

### Web server

A [Web server](http://www.javaworld.com/article/2077354/learn-java/app-server-web-server-what-s-the-difference.html) __handles the HTTP protocol__. When the Web server receives an HTTP request, it responds with an HTTP response, such as sending back an HTML page. 

To process a request, a Web server may __respond with a static HTML page__, or delegate the __dynamic response__ such as CGI scripts, JSPs (JavaServer Pages), servlets, ASPs (Active Server Pages), server-side JavaScripts, or some other server-side technology. 

### Application server

An [Application server](http://www.javaworld.com/article/2077354/learn-java/app-server-web-server-what-s-the-difference.html) __exposes business logic to client applications__ through various protocols, possibly including HTTP. The clients can include GUIs (graphical user interface) running on a PC, a Web server, or even other application servers. 

In most cases, the server exposes this business logic through a component API, such as __the EJB (Enterprise JavaBean) component model__ found on J2EE (Java 2 Platform, Enterprise Edition) application servers. 

Moreover, the application server manages its own resources. Such gate-keeping duties include security, transaction processing, resource pooling, and messaging. 

There's [a nice example](http://www.javaworld.com/article/2077354/learn-java/app-server-web-server-what-s-the-difference.html) as well. 

### Another explanation

Web server on the left. 

<table>
    <tbody><tr id="row1" title="Application Server vs Web Server comparison - What is it?"><td class="acol bg-color bg-img font-color">What is it?</td>                <td id="valtd1_1" class="vcol bg-color bg-img font-color">A server that exposes business logic to client applications through various protocols including HTTP.</td>
                <td id="valtd1_2" class="vcol bg-color bg-img font-color">A server that handles HTTP protocol.</td>
                </tr><tr id="row2" title="Application Server vs Web Server comparison - Job"><td class="acol bg-color bg-img font-color">Job</td>                <td id="valtd2_1" class="vcol bg-color bg-img font-color">Application server is used to serve web based applications and enterprise based applications(i.e servlets, jsps and ejbs...). Application servers may contain a web server internally.</td>
                <td id="valtd2_2" class="vcol bg-color bg-img font-color">Web server is used to serve web based applications.(i.e servlets and jsps)</td>
                </tr><tr id="row3" title="Application Server vs Web Server comparison - Functions"><td class="acol bg-color bg-img font-color">Functions</td>                <td id="valtd3_1" class="vcol bg-color bg-img font-color">To deliver various applications to another device, it allows everyone in the network to run software off of the same machine.</td>
                <td id="valtd3_2" class="vcol bg-color bg-img font-color">Keeping HTML, PHP, ASP etc  files available for the web browsers to view when a user accesses the site on the web, handles HTTP requests from clients.</td>
                </tr><tr id="row4" title="Application Server vs Web Server comparison - Supports"><td class="acol bg-color bg-img font-color">Supports</td>                <td id="valtd4_1" class="vcol bg-color bg-img font-color">distributed transaction and EJB's</td>
                <td id="valtd4_2" class="vcol bg-color bg-img font-color">Servlets and JSP</td>
                </tr><tr class="comparisonRow diff lastRow" id="row5" title="Application Server vs Web Server comparison - Resource utilization"><td class="acol bg-color bg-img font-color">Resource utilization</td>                <td id="valtd5_1" class="vcol bg-color bg-img font-color">High</td>
    <td id="valtd5_2" class="vcol bg-color bg-img font-color">Low</td>
</tr></tbody></table>

#### 

[[For J2EE](http://www.geekinterview.com/question_details/17043), Web server is used only for Jsp and Servlets and static functionality. It doesn't support EJB and JMS and JAAS.

Application server is basically: 

> AppServer = WebServer + EJB container. 

__Tomcat is web container__ where as Apache is web server.

An Application Server may include a Web Server inside it.
