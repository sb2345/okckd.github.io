---
layout: post
title: "[Design] Designing Scalable Systems (`)"
comments: true
category: Design
tags: [  ]
published: false
---

1. horizontal scaling

load balancer get all requests, and distribute to one of the back-end servers

user sees not DNS, but address of load balancer

all backend server must have identical information (the price you pay for scalability)

