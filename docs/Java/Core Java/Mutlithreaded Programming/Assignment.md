- Create a count class that has a count variable.
- Create two different classes `Adder` and `Subtractor`.
- Accept a count object in the constructor of both the classes.
- In `Adder`, iterate from 1 to 100 and increment the count variable by 1 on each iteration.
- in `Substraction`, iterate from 1 to 100 and decrement the count variable by 1 on each iteration.
- Print the final value of the count variable.
- what would the ideal value of the count variable be?
- what is the actual value of the count variable?
- try to add some delay in the `Adder` and `Subtractor` classes using inspiraiton from the code below. What is the value of the count variable now?
```Java
try{
	Thread.sleep(1000);
}catch(InterruptedException e){
	e.printStackTrace();
}
```

```Java
@Getter
@Setter
class Count{
	int count;
	public Count(){
		count = 0;
	}
	public Count(int num){
		count = num;
	}
	void increment(){
		count++;
	}
	void decrement(){
		count--;	
	}
}
```

```Java
class Adder implements Runnalbe{
	Count cnt;
	Thread t;
	public Adder(Count count){
		this.cnt = count;
		t = new Thread(this);
		t.start();
	}
	public void run(){
		for(int i=0;i<100;i++){
			cnt.increment();
		}
	}
}
```

```Java
class Subtractor implements Runnable{
	Count cnt;
	Thread t;
	public Subtractor(Count cnt){
		this.cnt = cnt;
		t = new Thread(this);
		t.start();
	}
	public void run(){
		for(int i=0;i<100;i++){
			cnt.decrement();
		}
	}
}
```

```Java 
class Main{
	public static void main(String [] args){
		Count count = new Count(5);
		Adder adder = new Adder(count);
		Subtractor sub = new Subtractor(count);
		adder.t.join();
		sub.t.join();

		System.out.println(count.getCount());
	}

}
```


Running the above code should ideally result in the count variable being 0. However, if you increase the number of iterations in the Adder and Subtractor classes, you will see that the count variable is not 0.