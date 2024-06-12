When two or more threads need access to a shared resource, they need some ay to ensure that the resource will be used by only one thread at a time.

- Key to synchronization is the concept of monitor.
- A *monitor* is an object that is used as a mutually exclusive lock. Only one thread can own monitor at a given time.
- When thread acquires a lock, it is said to have *entered* the monitor. All other thread will be suspended until the first thread exit. there other thread said to be in *waiting*.
- A thread that own a monitor can reenter the same monitor if it so desires.
We can synchronize our code in either of two ways.
1. Using [[#Synchronized Method]]
2. [[#The Synchronized Statement]]
### Synchronized Method

#### Without Synchronization.

```Java
class Callme{
	void call(String msg){
		System.out.println("["+ msg);
		try{
			Thread.sleep(1000);
		}catch(InterruptedException e){
			e.printStackTrace();
		}
		System.out.println("]");
	}
}
class Caller implements Runnable{
	String msg;
	Callme target;
	Thread t;
	public Caller(Callme targ,String s){
		this.target = targ;
		this.msg = s;
		t = new Thread(this);
		t.start();
	}
	public void run(){
		target.call(msg);
	}
}
```

```Java #Driver Class
class Main{
	public static void main(String args[]){
		Callme target = new Callme();
		Caller ob1 = new Caller(target,"Hello");
		Caller ob1 = new Caller(target,"Synchronized");
		Caller ob1 = new Caller(target,"World");
		try{
			obj1.t.join();
			obj2.t.join();
			obj3.t.join();
		}catch(InterrunptedException e){
			System.out.println("Interrupted");
		}
	}
}
```

Here is the Output produced by this program:
First run
```Output
[Hello
[World
[Synchronized
]
]
]
```
2nd Run
```Output
[Synchronized
[World
[Hello
]
]
]
```

---
#### After using synchronized keyword
To fix the preceding program, you must *serialize* access to **call()** method.
That is, you must restrict its access to only one thread at a time.

To *Serialize* such critical section, use **synchronized** keyword
```Java
class Callme{

    synchronized void call(String msg){
        System.out.print("["+ msg);
        try{
            Thread.sleep(1000);
        }catch(InterruptedException e){
            e.printStackTrace();
        }
        System.out.println("]");
    }
}
```

```Output
[Hello]
[World]
[Synchronized]
```

- synchronized keyword used for methods, to create synchronized methods.
- but that won't help in case of *serialize* accessing object. 
---

# The Synchronized Statement

synchronized statement used to make access of an object serialize.

- As synchronized method only serialize methods, but when in case resource that used by multiple thread and if we have need to make it serialize access then *Synchronized Statement* helps us.

**Syntax of Synchronized Statement**
```Java
synchronized(objRef){
	//statements to be synchronized
}
```
- Here objRef is a reference to the object being synchronized.

How to use Synchronized Statement
- Ask to solve concurrency problem, what object/resources need to access serially.
- In Above problem what object need to be serialize access.
	- it object of `Callme`, Right! 
- Now where it being accessed.
	- inside Caller -> run() method
- Means, we have use synchronized statement inside Caller class -> run() method.
```Java
class Caller{

	String msg;
	Callme target;
	Thread t;
	public Caller(Callme targ,String s){
		this.target = targ;
		this.msg = s;
		t = new Thread(this);
		t.start();
	}
	public void run(){
		synchronized(target){
			target.call(msg);
		}
		
	}
}
```
- This Code also produce same result as above. 

# Synchronization Problem Examples.
Problem Statement 1: Two Class(`Adder` and `Subtractor`) accessing same object(`Count`).
- we have  Adder and  Subtractor Class, both takes Count class object.
- Adder and Subtractor both run on separate thread.

```Java
class Count{
	private int count = 0;
	void increment(){
		count++;
		try{
			Thread.sleep(10);
		}catch(InterruptedExecption e){
			e.printStackTrace();
		}
	}
	void decrement(){
		count--;
		try{
			Thread.sleep(10);
		}catch(InterruptedExecption e){
			e.printStackTrace();
		}
		
	}
	int getCount(){
		return count;
	}
}
```
```Java
class Adder implements Runnable{
	Count count;
	Thread t;
	public Adder(Count cnt){
		this.count = cnt;
		t = new Thread(this);
		t.start();
	}
	public void run(){
		for(int i=0;i<100;i++){
			count.incremets();
		}
	}
}
```

```Java
class Subtractor implements Runnable{
	Count count;
	Thread t;
	public Subtractor(Count cnt){
		this.count = cnt;
		t = new Thread(this);
		t.start();
	}
	public void run(){
		for(int i=0;i<100;i++){
			count.decrements();
		}
	}
}
```

```Java #Main
class Main{
	public static void main(String [] args){
		Count count = new Count();
		Adder adder = new Adder(count);
		Subtractor subtractor = new Subtractor(count);
		try{
			adder.t.join();
			subtractor.t.join();
		}catch(IntrruptedException e){
			e.printStackTrace();
		}
		System.out.println(count.getCount());
	}
}
```

- ideally this program print Count = 0. but sometime count not equal to 0.
- **This is because of synchronization problem**.
### Solution
1. Using Synchronized Statement.
	- Count is being need to access serially.
		- objRef is count
	- Where I should write synchronized statement.
		- Where Count object is being accessed. There!
		- Inside run() method.
```Java
class Adder{
	//above code
	public void run(){
		for(int i=0;i<100;i++){
			synchronized(count){
				count.increment();
			}
		}
	}
}
```
2. Synchronized Method
	- We make method `increment` and `decrement` method synchronized.
```Java
class Count{
	private int cnt = 0;
	synchronized void increment(){
		cnt++;
	}
	synchronized void decrement(){
		cnt--;
	}
	int getCount() {
		return cnt;
	}
}
```