---
layout: post
title: "[Octopress] Clone Octopress Blog From A Different Computer"
comments: true
category: Design
tags: [ cc150 ]
---

I've had a little confusions about how to develop my Octopress blog on 2 different computers. Some solutions posted online does not work, and it turns out that some commands have changed its functions in new version of Octopress. So, I write this post to clarify these confusions. 

To set up a new local repository from an online github octopress blog repo, follow the instructions: 

1. __clone the source branch to the local octopress folder__
> git clone -b source git@github.com:willran168/willran168.github.io.git octopress

1. __run the rake installation to configure everything__
> cd octopress
> gem install bundler
> rbenv rehash    (I think this is optional)
> bundle install
> rake setup_github_pages

1. __enter repository URL__
> git@github.com:willran168/willran168.github.io.git

1. __clone the master branch to the _deploy subfolder__
> git clone git@github.com:willran168/willran168.github.io.git _deploy 

Clone master branch is the last step. Because running `rake setup_github_pages` will remove previous _deploy folder and init a new repo inside of it. So master have to be cloned after this step. 

It's done. Now we can do 'rake gen_deploy', or 'git commit or push origin source'. 

[reference](http://blog.zerosharp.com/clone-your-octopress-to-blog-from-two-places/)
