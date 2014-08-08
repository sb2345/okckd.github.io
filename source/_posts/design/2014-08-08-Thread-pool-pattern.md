---
layout: post
title: "[Design] Thread pool pattern"
comments: true
category: Design
tags: [  ]
---

### Overview

[Thread pool](http://programmers.stackexchange.com/a/173580) is a collection of managed threads usually organized in a queue, which execute the tasks in the task queue.

{% img middle /assets/images/thread-pool.png %}

[A sample thread pool](http://en.wikipedia.org/wiki/Thread_pool_pattern) (green boxes) with waiting tasks (blue) and completed tasks (yellow)

### Why Thread Pool?

[Many server applications](http://www.ibm.com/developerworks/library/j-jtp0730/), such as __Web servers (eg. Tomcat)__, database servers, file servers, or mail servers must process a large number of tasks received from a network protocol. Often, the task is short-lived and the number of requests is large. 

__Thread Pools are useful when you need to limit the number of threads__ running in your application at the same time. 

### More details

A thread pool is a group of pre-instantiated, idle threads which stand ready to be given work. These are preferred over instantiating new threads for each task when there is __a large number of short tasks__ to be done __rather than a small number of long ones__. 

Instead of starting a new thread for every task to execute concurrently, the __task can be passed to a thread pool__. As soon as the pool has any idle threads the task is assigned to one of them and executed.

Thread pools are often used in multi threaded servers. Each connection __arriving at the server via the network is wrapped as a task__ and passed on to a thread pool. The threads in the thread pool will process the requests on the connections concurrently.

### Code

__a [simple thread pool implementation](http://tutorials.jenkov.com/java-concurrency/thread-pools.html)__

Pool Class: 

	public class ThreadPool {

	  private BlockingQueue taskQueue = null;
	  private List<PoolThread> threads = new ArrayList<PoolThread>();
	  private boolean isStopped = false;

	  public ThreadPool(int noOfThreads, int maxNoOfTasks){
	    taskQueue = new BlockingQueue(maxNoOfTasks);

	    for(int i=0; i<noOfThreads; i++){
	      threads.add(new PoolThread(taskQueue));
	    }
	    for(PoolThread thread : threads){
	      thread.start();
	    }
	  }

	  public void synchronized execute(Runnable task){
	    if(this.isStopped) throw
	      new IllegalStateException("ThreadPool is stopped");

	    this.taskQueue.enqueue(task);
	  }

	  public synchronized void stop(){
	    this.isStopped = true;
	    for(PoolThread thread : threads){
	      thread.stop();
	    }
	  }
	}

Thread Class: 

	public class PoolThread extends Thread {

	  private BlockingQueue taskQueue = null;
	  private boolean       isStopped = false;

	  public PoolThread(BlockingQueue queue){
	    taskQueue = queue;
	  }

	  public void run(){
	    while(!isStopped()){
	      try{
	        Runnable runnable = (Runnable) taskQueue.dequeue();
	        runnable.run();
	      } catch(Exception e){
	        //log or otherwise report exception,
	        //but keep pool thread alive.
	      }
	    }
	  }

	  public synchronized void stop(){
	    isStopped = true;
	    this.interrupt(); //break pool thread out of dequeue() call.
	  }

	  public synchronized void isStopped(){
	    return isStopped;
	  }
	}

An explanation: 

> The thread pool implementation consists of two parts. A ThreadPool class which is the public interface to the thread pool, and a PoolThread class which implements the threads that execute the tasks.

> To execute a task the method ThreadPool.execute(Runnable r) is called with a Runnable implementation as parameter. The Runnable is enqueued in the blocking queue internally, waiting to be dequeued.

> The Runnable will be dequeued by an idle PoolThread and executed. You can see this in the PoolThread.run() method. After execution the PoolThread loops and tries to dequeue a task again, until stopped.

> To stop the ThreadPool the method ThreadPool.stop() is called. The stop called is noted internally in the isStopped member. Then each thread in the pool is stopped by calling PoolThread.stop(). Notice how the execute() method will throw an IllegalStateException if execute() is called after stop() has been called.

> The threads will stop after finishing any task they are currently executing. Notice the this.interrupt() call in PoolThread.stop(). This makes sure that a thread blocked in a wait() call inside the taskQueue.dequeue() call breaks out of the wait() call, and leaves the dequeue() method call with an InterruptedException thrown. This exception is caught in the PoolThread.run() method, reported, and then the isStopped variable is checked. Since isStopped is now true, the PoolThread.run() will exit and the thread dies.

