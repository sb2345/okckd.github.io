---
layout: post
title: "[NineChap Sys] System Design Class 1 "
comments: true
category: NineChap

---

# System Design

## defination 

the process of defining the __architecture, components, modules, interfaces and data__ to satisfy specified __requirements__. 

1. conceptual design (macro)
2. logical design
3. physical design (micro)

### Top-down design

Eg. MS Office, Huawei Security System

### Bottom-up design

Most start-up use, MVP first using Medetor + MongoDb. 

## 5 steps (SNAKE Principle):

1. __Scenario__: case/interface - input
1. __Necessary__: constrain/hypothesis - input
1. __Application__: service/algorithm - output
1. __Kilobit__: data - output
1. __Evolve__ - solution

# A top-down example

Example one: __design a radio__

## Step One, Scenario

1. brain storm

    1. register/log in
    1. play music
    1. recommendation

1. prioritize

    1. play music
        1. Get channel
        1. select a channel
        1. play

## Step Two, Necessary

1. ask

    1. total user - 100,000,000
    1. __daily users - 1,000,000__

1. predict

    1. user analysis
    1. Traffic analysis
    1. Memory analysis
    1. QPS

Details:

1. user analysis

    > Avg Concurrent users = daily users __/ 5__ = 200,000
    >
    > Peak Concurrent users = concurrent user __\* 3__ = 600,000

    considering your product may grow in the next 3 month:
    
    > Max Peak users in 3 month = Peak users __\* 10__ = 6,000,000

1. Traffic analysis

	> Request of new music per user: 1 music/min
	>
	> Music size = 3MB
	>
	> Max peak traffic (in 3 months) = 6,000,000 \* 3MB / 60 = 300GB/s

1. Memory analysis

	> Memory per user (metadata) = 10KB
	>
	> Max daily memory = 1,000,000 \* 10 \* 10 = 100 million KB = 100GB
    >
    > (10 times of avg daily user)

## Step Three, Application

1. Replay the case, one service for each
1. Merge the services

{% img middle /assets/images/design-class1-basic-receptionist.png %}

## Step Four, Kilobit: data

1. Append 1 dataset for each service

    Eg. User service: stability, more addition, less modify and deletion.

    Eg. Channel Service: high concurrency, MongoDB

    Eg. Music Service: MP3 File Systems

{% img middle /assets/images/design-class1-reco-5.png %}

## Last Step, Evolve

1. Better: constrains 

    eg. able to handle 300GB/s traffic?

1. Broader: new cases

    share music? delete user account?

1. Deeper: details design

From views of __Performance, Scalability and Robustness__.

{% img middle /assets/images/design-class1-snake.jpg %}

# A bottom-up example

Example two: __design a recommendation module__

## A simple algo: 

    u1={m3,m5,m7,m11}
    u2={m1,m2,m3,m4,m5,m6,m7,m8,m9}
    Similarity( u1, u2 ) = 3
    
m - music

u - user

Similarity = # of same music for different users

## Adv algo: 

find his __top-1 similar user__. Stay tuned for future posts. 

## Use the 5 Steps (SNAKE)

1. Step One, Scenario
1. Step Two, Necessary
1. Step Three, Application
1. Step Four, Kilobit: data
1. Last Step, Evolve

Because this question is relatively easy, we will not do case-analysis (Macro). 

__Instead, we do micro design__ by starting at the interface. 

## Step One, Scenario

Interface 

    class Recommender {
        public int findSimilarUser(int userId) {
            //
        }
    }

## Step Two, Necessary

1. ask
    1. total users = 100,000,000
    1. total music = 10,000,000
    1. peak users in 3 month = 6,000,000
    
    However, not everyone is logged in. Thus we won't need to recommend for everybody. On average, the logged-in ratio is 1% - 30%. Let's assume 5%. 
    
    1. participation percentage = 5%
    
    And user's interest won't change every minute. Let's recalculate only after 10 minutes.
    
    1. calculation frequency = 1 update/10min/user

1. predict

    1. user analysis (skip)
    1. Traffic analysis (skip)
    1. Memory analysis (skip)
    1. QPS
    
    Peak QPS = 6,000,000 \* 5% / (10 \* 60) = 500/s

## Step Three, Application

__The simpliest algorithm: BF compare__. The complexity is O(m n) for each user, where m is # of music a person likes, and n is # of total users. For k users, it takes O(k m n) time (k can be = peak concurrent users). 

This is roughly 0.2s per user. Thus __Max QPS = 5__. 

> One word about complexity-to-seconds estimation. 
>
> O(n ^ 3) -> 1s
>
> O(n ^ 2) -> 0.2s
>
> O(n) -> 20ms
>
> O(k) -> k ms

## Step Four, Kilobit: data

Very simple:

{% img middle /assets/images/design-class1-reco-1.png %}

## Last Step, Evolve

Read on. 

# How to go from Level 0 to Level 1

Refer to the previous question. How can we improve???

1. performance
1. scalability
1. robustness

## performance

A better algo: Inverted Index

{% img middle /assets/images/design-class1-reco-2.png %}

Avg performance increase to ~ 20ns (with some optimization of MapReduce procedure, discuss later). 

__Max QPS increase to 50__. 

## scalability

Use a __dispatcher__ to re-direct the requests to multiple machines. 

{% img middle /assets/images/design-class1-reco-3.png %}

### How many machines do we need then? 

Well we need 500 QPS. The algo above achieves ~ 50 QPS. __Should we need 10 machines__?

The answer is NO. A machine with 8 (or 16) core CPU could be able to handle. 

We can also have a __hot-standby__, to be safe. 

> hot standby is used as a failover mechanism to provide reliability in system configurations. 
>
> When a key component fails, the hot spare is switched into operation. 

## robustness

Tips about system design for senior engineers: 

> __Draw 1 machine first__. This machine can contains multiple datasets and run multiple processes. 
>
> On top of this machine, the interface layer is __one single Manager process__. The Manager is in charge of almost everything: handling data lost, handle high concurrency, copy multiple instance of itself... 
>
> Like this: 

{% img middle /assets/images/design-class1-reco-6.png %}

### Back-end

Now we need __a cluster of datasets__ (which has Manager on top of it), and __a cluster of Recommenders__. Manager is in charge of copying multiple instances. 

Dataset can be put in different physical locations. Recommender don't really need, cuz it's only do calculation job. 

### Receiving requests

Just now we used __Receptionist (or Dispatcher)__ to handle request. Now we use a __Web service__ (eg. Apache). It's not necessary to make it a cluster. 

### Big Brother

We need a __monitor system__ to oversee everything. 

Also, Big Brother is in charge of heart-beat. If not received, Big Brother have some double-check machanism. 

{% img middle /assets/images/design-class1-reco-4.png %}

### Connecting the dots

__Dispatcher__ is used to connect the 4 components. It's like a messaging queue that collects and distributes jobs among everybody (eg. control and distributed info). 

It can be stateful or stateless. 

Keep in mind __the connection between Dataset and Recommender__ remains. It's slow going thru Dispatcher. 

### Distribute it

During development, the 5 components can be put on same machine. When we deploy distributely, we use __Socket connection (keep alive)__ to connect them. 

Notice the Web Service is __connection heavy__, which consume large CPU and RAM resource. It's better to seperate to one machine. 

Big brother is read/write heavy, so it's OKAY to put on same machine with Dispatcher. 

Since Dataset and Recommender have data exchange, it's a good idea to put on same machine. 

### Additional questions

Implement Dispatcher with __consumer-producer__ model. 
