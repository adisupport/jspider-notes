Thread is Smallest unit of processing. Thread is what processor executes at a time.
Multithreading in Java is a process of executing multiple threads simultaneously.

we use multithreading than multiprocessing because threads use a shared memory area. They don't allocate separate memory area so savs memory, and context-switching between the threads takes less time than process.

Java Multithreading is mostly used in games, animation, etc.
![[Pasted image 20240318120512.png]]
As shown in the above figure, a thread is executed inside the process. There is context-switching between the threads. There can be multiple processes inside the OS, and one process can have multiple threads.

Note: At a time one thread is executed only.


# How to create a thread in Java

There are two ways to create a thread:
	1. By extending Thread class
	2. By Implementing Runnable interface.
### Thread Class
Constructors of Thread Class:
- Thread()
- Thread(String name)
- Thread(Runnable r)
- Thread(Runnable r, String name)
  -These are Commonly used Constructors of Thread Class.
Commonly used Method of Thread class:
1. Thread Basic Methods  
	- void run():
	- void start():
	- void sleep(long milliseconds)
	- void join():waits for a thread to die.
	- join(long milliseconds):waits for a thread to die for the specified milliseconds.
	- String getName(): return the name of thread.
	- String setName(): change name of thread.
	- int getId(): return the id of thread.
	- void yield(): Cause the currently executing thread object to temporarily pause and allow other threads to execute.
2. methods that related to life cycle of threads.
	- void resume()
	- void isAlive()
	- void interrupt()
	- boolean isInterrupted()
	- static boolean interrupted()
	- Thread.State.getState()
3. Thread Priority related methods
	- void setDaemon(boolean b): mark the thread as daemon or user thread.
	- boolean isDaemon() : tests if the thread is a daemon thread.
	- int getPriority(): return the priority of the thread.
	- int setPriority(int priority): changes the priority of the thread.
### Runnable interface

The Runnable interface should be implemented by any class whose instances are intended to be executed by a thread.Runnable interface have only one method named run():

1. public void run(): is used to perform action for a thread.
### Starting a thread:

The `start()` method of Thread class is used to start a newly created thread. it performs the following tasks:
- A new thread start (with new callstack)
- the thread moves from New state to the Runnable state.
- When the thread gets a chance to execute, its target run() method will run.

# Hello Thread Program 
#### 1. Thread Class

 ```Java
 class ThreadExample extends Thread{
    public void run(){
        for(int i=0;i<10;i++){
            System.out.print(i+", ");
        }
    }
}
class Main{
	public static void main(String args[]){
		//Creating a Object
		ThreadExample tExample = new ThreadExample();
		//Start a thread and call the run method.
		tExample.start();
	}
}
```
Explanation:
- created `ThreadExample` class and extends with `Thread` class.
- Implemented `public void run method`.
- created object into main method. `ThreadExample tExample = new ThreadExample().`
- start the thread by `tExample.start()` method.
- When `tExample.start()` will called into main method new thread being created and execute `tExample.run()` method.

#### 2. Runnable Interface
Runnable Interface has one method `public void run()`.
```Java 
interface Runnable{
	void run();
}
```

implemented Runnable interface  
```Java
class RunnableExample implements Runnable{
    public void run(){
        System.out.println("Hello From RunnableExample");
    }
}
class Main{
	public static void main(String []args){
		Runnable rExample = new RunnableExample();
		Thread t1 = new Thread(rExample);
		t1.start();
	}
}
```

Explanation:
- created `RunnableExample` class which implemented Runnable interface.
- `Runnable rExample = new RunnableExample();` 
- `Thread t1 = new Thread(rExample)` create a object and passed to Thread Constructor.
- `t1.start()` which start Thread.