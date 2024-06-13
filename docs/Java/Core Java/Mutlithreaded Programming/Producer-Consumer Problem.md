The Producer-Consumer Problem is a classic synchronization problem in operating Systems.
### Problem Statement
![Problem Statement Diagram](https://camo.githubusercontent.com/fee4a2b8cdcb3298d8a6212878552223d3553d091553470dbad25517e6a73ab1/687474703a2f2f70616765732e63732e776973632e6564752f7e626172742f3533372f6c6563747572656e6f7465732f666967757265732f73362d70726f64636f6e732e6a7067)
- we have a fixed-size of buffer and a Producer Process/Thread, and a Consumer Process/Thread.
- The Producer process create an item and adds it to the shared buffer.
- The Consumer Process takes items out of the shared buffer and "consumes" them.
- Producer process must not produce an item if the shared buffer is full.
- Consumer Process must not consume an item if the shared buffer is empty.
```Java
class Producer{
	String buffer[20];
	Thread t;
	public  Producer(String buffer[]){
		this.buffer = buffer;
		t = new Thread(this);
		t.start();
	}
	public void run(){
		buffer.add(new String("add to buffer"));
	}
}

class Consumer{
	String buffer[20];
	Thread t;
	public Consumer(String buffer[]){
		this.buffer = buffer;
		t = new Thread(this);
		t.start();
	}
	public void run(){
		buffer.pop();
	}
}
```

```Java
class Main{
	public static void main(String args[]){
		String buffer[20];
		
	}
}
```