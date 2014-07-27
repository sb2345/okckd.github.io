---
layout: post
title: "[Design] How we've scaled Dropbox (`)"
comments: true
category: general
tags: [  ]
published: false
---

## Overview

### Challenges 

1. write volumn - read/write ratio, eg. twitter have 1000-1 read-write ratio. But Dropbox is around 1-1 read-write. Have multi-petabyte cache on the server.

1. Can't be wrong - file security and completeness can't be wrong

### High-level architecture

1. Possibly GFS - google file system

1. In mid-2007: 2 employee + 1 backend + 0 user 

    web server + application server, static content, and file content of all users

1. In late-2007: 3 employee + 1 backend + 0 user
    
    Put server on DB server and Amazon S3. 

1. In early-2008: 4 employee + 2 backend + 50k users

    Around 20', I start to don't understand. 

https://www.youtube.com/watch?v=PE4gwstWhmc
