---
layout: post
title: "[Design] Speed Up Webpage for Slow Connection (2) "
comments: true
category: Design
tags: [  ]
---

[ref](www.geeksforgeeks.org/amazon-interview-set-72-campus-sde-1)

### Question

> Suppose you are handling Amazon website and you have 10 MB size home page. Optimize the homepage for a customer who has 100 kbps internet connection.

> Further he asked for the customer who has 100 mbps internet connection.

### Website KPI

There are [3 interesting phases](https://community.compuwareapm.com/community/display/PUB/Best+Practices+on+Web+Site+Performance+Optimization) of a web site from an end-user performance perspective. 

1. First Impression
1. OnLoad 
1. Fully Loaded Time.

### Loading Time

__Question: what percentage of the time a user spends waiting for your page to load is spent after the HTML comes back to their browser__? 

It is typically __[over 90%](http://www.sitepoint.com/seven-mistakes-that-make-websites-slow/)__. 

Most of the time users spend waiting on your website is spent after the HTML page has been retrieved by their browser. 

#### Fetching the HTML is just the beginning

__In a nutshell, browsers parse your page’s HTML, sequentially discovering its assets__ (such as scripts, stylesheets, and images), requesting and then either parsing and executing them or displaying them as appropriate. 

But these assets are not simply fetched all at once. Instead, the __browser opens a limited number of connections to the server(s)__ referenced by the page. There is __overhead involved in establishing TCP and HTTP connections__, and some __unavoidable latency__ in pushing the request and response bytes back and forth across the network.

So, in general, round trips between the browser and server are expensive. The structure of the HTML markup, the number and the ordering of its assets, are absolutely critical factors in its performance.

### What hijacks your load time

#### 1. Too Many HTTP Requests

This is the single biggest contributor to performance problems in most web pages. 

1. Concatenate scripts and stylesheets

1. Combine images with sprites (put common images into a single large image file, then use CSS to position and selectively display the appropriate portion of the sprite image)

1. Use fewer images, more CSS. 

#### 2. Minimal Client-side Processing

1. Validation on client. (eg. form input)

1. Use web standards and MVC separation, making a maintainable, accessible, future-proof and max-performance website. 

    Think of the HTML as the model, the CSS as the view, and the JavaScript as the controller. This separation tends to make code more efficient and maintainable, and makes many optimization techniques much more practical to apply.

1. Push presentation code into the client tier (eg. Charts and graphs — push raw data to the client in JSON format, and use JavaScript and CSS to create pretty graphs.)

1. Leverage Ajax techniques (only requiring small parts of the page to change in response to user actions)

#### 3. Low Number of Parallel Requests

Fetch a script, parse and execute it, then fetch another one... this will use up all the available connections. There are things you can do to your HTML to allow virtually any browser to make many requests at once, which has a huge impact on latency.

1. Use browser-appropriate domain sharding

1. Use intelligent script loading

1. Leverage Keep-Alive (reuse the same TCP connection for multiple HTTP request/response cycles)

#### 4. Failure to leverage browser cache / local storage

1. [HTTP cache overview](http://www.mnot.net/cache_docs/)

1. Leverage local storage

#### 5. Third-party widgets

1. Avoid third-party widgets!
1. Try to use widgets that provide asynchronous implementations, so their inevitably terrible performance impacts their widget without dragging down your entire UX with it.

#### 7. Failure to Use a Global Network

Amazon S3. 

Ref: http://www.sitepoint.com/seven-mistakes-that-make-websites-slow/
