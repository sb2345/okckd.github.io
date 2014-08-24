---
layout: post
title: "[Design] Java Web Development (`)"
comments: true
category: Design
tags: [  ]
published: false
---

## Overview

#### Container

Java web application runs inside a container on the server. This container runs on the server. The container provides a runtime environment for Java web applications (just like a JVM, although container runs JVM).

Java distinguishes two containers: the web container and the Java EE container. Typical web containers in the Java world are Tomcat or Jetty. Most of the modern Java web frameworks are based on servlets and JavaServer Pages. Popular Java web frameworks are JavaServer Faces, Struts, Spring. These web frameworks usually run in a web container.

#### Servlet

A servlet is a Java class which __extends "HttpServlet" and answers a HTTP request__ within a web container.

#### JavaServer Page

JavaServer Pages (JSP) are files which contain HTML and Java code. The web cotainer __compiles the JSP into a servlet__ at the first time first time the JSP is accessed.

