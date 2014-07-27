---
layout: post
title: "[Question] Elephant And Bananas"
comments: true
category: General
tags: [ unit test needed ]
---

### Question 

[link](http://tech-queries.blogspot.sg/2011/04/elephant-and-banana.html)

> There's a elephant, which can carry max 1000 bananas. The elephant eats a banana every 1 Km (both forward and back).

> Now we want to transfer 3000 bananas to a place 1000 Km away. How many bananas can be left? 

> Also solved to generalized problem (write code for solution).

### Analysis

__If we subdivide distances for each kilometer__. Notice if elephant wants to shift all the bananas 1 km, __you will loose 5 bananas every km__. 

So we transferred 2995 (998+998+999) to one km distance. This process continues until after 200 km, we have only 2000 bananas left with remaining distance of 800 km. 

__Start from here, we only loose 3 bananas every km__. This goes on for another 334 km, we will have 998 bananas left, and the rest of the bananas can be transfered in a single journey. 

### Solution

__532 bananas__. 

### Code

__not written by me__

    double transferBananas(double N, double D, double C, double F) {  
        // base case: remaining bananas <= C,  
        // so carry all the bananas in one trip  
        // at this point if distance is more than N/F,  
        // elephant can never reach destination, return 0  
        if (N <= C) {
            double bananasAtDestination = N - D*F;  
            return (bananasAtDestination >= 0.0) ?  
                bananasAtDestination :  0.0;    // out of bananas!  
        }  

        // # trips you would travel back and forth  
        int numTrips = 2*(ceil(N/C) - 1) + 1;  

        // how many bananas you consume per km  
        double costPerKm = numTrips * F;  

        // remaining number of bananas after consumption, we want it  
        // as an integer multiple of C.  
        double remainingBananas = C*(ceil(N/C) - 1.0);  

        // this is the distance you are able to travel before you  
        // reach ONE LESS round trip fetching bananas  
        // derived from eq: N - costPerKm * traveled = remaining bananas  

        double traveled = (N - remainingBananas) / costPerKm;  

        // we are able to travel greater (or equal) than the remaining  
        // distance, so fetch the bananas right to the destination  
        if (traveled >= D)
            return N - D*costPerKm;  

        // calculate recursively as we travel ONE less round trip now.  
        return transferBananas(remainingBananas, D-traveled, C, F);  
    }
