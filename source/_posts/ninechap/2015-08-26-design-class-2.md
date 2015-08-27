---
layout: post
title: "[NineChap Sys] System Design Class 2 "
comments: true
category: NineChap

---

# Overview

This class covers database design: 

1. design data with class and inheritance
1. design a user system (Netflix 2015)
1. design a payment system (Yelp, BigCommerce 2015)

# Example One

__design account (login/out) system__ for our radio. 

## Step one, scenario

1. register, update, remove account
1. login/out
1. user balance, VIP services

## Step Two, necessary

1. Ask
	
	1. total user: 100 million
	1. daily user: 1 million
	
1. predict

	1. daily active user in 3 month: 10 million
	1. register percentage: 1%
	1. daily new register: 100 thousand

1. more predict

	1. login percentage: 15%
	1. average login frequency: 1.2 (ppl may input wrong password 20% of time)
	1. daily login attempts: 10 million * 15% * 1.2 = 1.8 million
	1. average login frequency: 1.8 million / 24hr = 21 login/sec
	1. normal login frequency: 21 * 2 = 42 login/sec
	1. peak login frequency: 42 * 3 = 126 login/sec

## Step Three, Application

{% img middle /assets/images/design-class2-app-design.png %}

## Step Four, Kilobit

Data - User table should contain name and password. What else? 

    class User {
        int userId; (primary key)
        String name;
        String password;
    }

Data - User Table

    class UserTable {
        list<User> table;

        public insert(){}
        public delete(User){}
        public update(User){}
        public User select(){}
    }

> __[CRUD](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete)__, (Sometimes called SCRUD with an "S" for Search) are the four basic functions of persistent storage.

# Step Five, Evolve

## advanced 2: __verification and forbidden accounts__

We have to know the concept of __Account State Lifecycle Graph__:

{% img middle /assets/images/design-class2-account-life-cycle.png %}

1. ban: fake user, advertising users... bannned by the management

1. inactive: user choose to suspend his own account, voluntarily.

1. delete account: normally we won't remove all related data (just make userId as "deleted"). Otherwise a lot of data can be violated. All your chatting history __actually remains__. 

### redesign User Table

Old User table:

    class User {
        int userId; (primary key)
        String name;
        String password;
    }

Modified User table:

    class User {
        int userId;
        char name[10];
        char hiddenPassword[10];
        int state;
    }

1. We added state, to support Account life cycle. 

1. We changed username to fixed size, for better performance on searching and storing. Can prevent certain attacks, too. 

1. save encrypted password. 

## advanced 3: login/out process

1. User account auto logged out after a certain period of time.
1. multiple account logged in at same time.

{% img middle /assets/images/design-class2-session-life-cycle.png %}

### Session

__Session is a conversation__ between user and server. 

1. User can have >1 session, if he log in from different devices.
1. Session must be verified, thus we have to keep __sessionId__.

Session status: "iPad online", "PC online"...

Modify User table: 

    class User {
        int userId;
        char name[10];
        char hiddenPassword[10];
        int state;
        List<session> sessionList;
    }

Important in Session table:

1. device ID
1. time-out period

    class Session {
        private sessionId;
        int userId;
        
        int deviceCode;
        long timeOut;
    }

User table would include a __session list__. 

### further improvement: session

1. we update sessionList very frequently.
1. size of sessionList is dynamic.

Solution: seperate the table. 

{% img middle /assets/images/design-class2-user-session-table.png %}

Question: When to clean up the session data (considering huge amount of data and frequent calculation)?

> Answer: every end of day. Or store sessions in-memory, so it lose all the data when machine restarts (it is used in Gaming platforms). Or we can clean up one user's session list whenever the user did a new log-in. 
>
> We do not remove session whenever it expires. It's too much calculation. 

### further improvement: inheritance

Apply inheritance to UserTable and SessionTable: 

    class Table {
        list<Row*> table;

        public insert(){}
        public delete(){}
        public update(){}
        public User select(){}
    }

    class UserTable extends Table {
    }
    
    class SessionTable extends Table {
    }

As for the Row class:

    class Row {
        List<Attributes> row;
    }
    
    class User extends Row {
    }
    
    class Session extends Row {
    }

## advanced 4: search in table

1. find my userId
1. find my userId range

Solution 1: add __HashMap__ in the table. Can do search in O(1), but can't find range. 

Solution 2: __BST data structure__. Can do search range and search in O(log2 n) time. 

### Best solution: B+ tree

__[B+ tree](https://en.wikipedia.org/wiki/B%2B_tree)__ - everything in O(logb n) which is __close to constant time__. 

Plus, B+ tree is hard disk friendly. Read more on a future post. 

## advanced 5: VIP services

User could buy VIP services using his acccount balance. 

    class ProService {
        int userId;
        double money;
        long endTime;

        public addMoney(){}
        public buyPro(){}
    }

### Q5.1: System crashes before adding time

Solution: __transaction with log__

    WriteLOG
    Transaction_1123: BEGIN
    money=20; endTime=16_07_2016

If system crash happens here, system will read the log, recover and roll back all original data. Try not to complete the transaction - just fail it. 

    WriteLOG
    Transaction_1123: BEGIN
    money=20; endTime=16_07_2016
    WriteLOG
    Transaction_1123: END
    money=10; endTime=16_08_2016

> What happens if system crash during writing the log? or during the rollback?

### Q5.2: check list

1. one user id have 2 corresponding pro-services information.
1. Shallow user: a pro-services info does not have corresponding user. 

Solution: have a checker class.

### Q5.3: 2 simutaneous purchase. 

Solution: lock. 

1. first process lock money & endTime.
1. Read money = 20
1. another process try to lock, but end up waiting (sleeping).
1. first process do the job, and release the lock. 
1. another process wakes up. 

> lock have time-out settings. It can be applied in distributed system as well. 

Question: does lock make your execution slow?

1. If another process is sleeping, CPU will be fully consumed by other process. So it won't impact. 

1. You can do some async processing, too. 

1. When you lock, try to lock only a small piece of code, not the entire method. In DB, lock only a row, not a table. 

1. Java [CAS](https://en.wikipedia.org/wiki/Compare-and-swap) (Compare and swap ) 

### Q5.4: machine crash

Solution: duplication. 

1. How many copies?

    Google did 3. Normally 2 in same data center, and 1 in another location. 
    
    Backup data normally is on another machine. But there's also [RAID](https://en.wikipedia.org/wiki/RAID) (redundant array of independent disks) which:
    
    > combines multiple physical disk drive components into a single logical unit for the purposes of __data redundancy, performance improvement__, or both. 

1. When does the copy happen? 

    Option 1 is __doing everyday nightly__. This is called a 'check point'.
    
    Option 2 is use another server to support __Shadow Redundancy__. All data from Machine 0 will be copied to Machine 1 WHILE it happens. The result is, Machine 1 is identical to Machine 0. If Machine 0 crashes, Machine 1 may be behind less than 1 second. 
    
    The way to duplicate is either re-play all the actions, or to read Machine 0's log and apply the new data. 

1. How to copy?

    User send data to 1 server, and from that server, pipeline. This ensures good usage of server bandwith, and serial transfer of data ensures low latency (several ms). 
    
    It's also possible to do tree-like transfer, but the above method is preferred cuz all machine consume same bandwidth.

1. What is log?

    It is actually 'checkpoint' + log. It allows you to rollback.

Data redundancy - Summary:

{% img middle /assets/images/design-class2-data-redundancy-1.png %}

### Final note: Data inconsistency

Main sources of inconsistency comes from:

1. network fault
1. disk error

The disk eror is solved by __checksum__ (compare during disk writing). 

# Summary

__[ACID](https://en.wikipedia.org/wiki/ACID) (Atomicity, Consistency, Isolation, Durability)__  is a set of properties that guarantee that database transactions are processed reliably. 

1. __Atomicity: all or nothing__

    Q5.1: System crashes before adding time
    
1. __Consistency__: validate according to defined rules

    Q5.2: check list
    
1. __Isolation__: independency between transactions __(lock)__

    Q5.3: 2 simutaneous purchase. 
    
1. __Durability__: stored permanently

    Q5.4: machine crash

{% img middle /assets/images/design-class2-summary.png %}

Question:

1. design a user system (Netflix 2015)

Hint: table design, register, login/out, password check, find password. 

1. Design payment system (Yelp, BigCommerce 2015)

Hint: the question does not ask about table/ds design itself, but rather the problems associated with payment. Read about ACID principle. 
