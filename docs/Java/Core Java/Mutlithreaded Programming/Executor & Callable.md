# Callable
If we want to execute a task that return a result, We can use the callable interface.
Callable interface is a functional interface that has only one method
```Java
public interface Callable<V>{
	v call() throws Exception;
}
```

Implement Callable with Functional Interface.
```Java
Callable<Integer> sumTask = () -> 2 + 3;
```

Implement Callable with class.
```Java
class SumThread implements Callable<Integer>{
	public Integer call() throw Exception{
		return 2 + 3;
	}
}

Callable<Integer> sumTask = new SumThread();
```

# How to Execute Callable

```Java
ExecutorService executorService = Executors.newCachedThreadPool();
Future<Integer> future = executorService.sumbit(sumTask);
Integer result = future.get();
```

- `Executors.newCachedThreadPool`: return `ExecutorService` object.
- `executorService.submit(sumTask)`: `Executor` use concept of thread pool. `executorService`handle assigning task to idle threads in thread pool and return `Future object`. 
- `Future<V>` class is used for asynchronous tasks it does not block code until you call `future.get()` method. 
- `<V> future.get()` : block the execution until the future has the value, then return it.



# Executor

The `Executor` interface is used to execute tasks. It is a generic interface that can be used to execute any kind of task.

```Java
public interface Executor{
	void execute(Runnable command);
}
```

`Executor` has only one method. so it is also functional interface.
- It takes Runnable object. 
- Executors internally use a thread pool to execute the tasks.
- The `void execute()` method is non-blocking. It return immediately after submitting the task to the thread pool.
- execute method is used to execute tasks that do not return a result.

# `ExecutorService`

The `Executors` interface has a **static** method called `newCachedThreadPool` that return `ExecutorService` object.

- The `ExecutorService` interface extends the Executor interface. 
- The `ExecutorService` interface has methods to execute tasks that return a result.
- The `ExecutorService` interface also has methods to shutdown the thread pool.
```Java
Executor executorService = Executors.newCachedThreadPool();
executorService.execute(()->System.out.println("Hello World"));
```
- Task that return results ![[#How to Execute Callable]]
>[!note] Task that return a result. #CallableSummary
>Tasks that return a result for that we have `Callable` interface and `ExecutorService` Executor.
>##### Creating a task
>	`Callable<Integer> task = ()->{return 5 + 7};`
>
> ###### Creating ExecutorService object.
> 	ExecutorService executorService = Executors.newCachedThreadPool(); 
> ##### Executing
> 	`Future<Integer> future = executorService.submit(task);`
> ###### Accessing result
> 	Integer result = future.get();
> - `future.get()` is Blocking code.

# Cancel Tasks
Future can be used to cancel task. the Future interface has a method called `cancel` that can be used to cancel a task.
The `cancel` method takes a `boolean` parameter. 
- `future.cancel(true)` : task is cancelled even if task is already running.
```Java
ExecutorService executorService = Executors.newCachedThreadPool();
Future<Integer> future = executorSrevice.submit(()->2+3);
future.cancel(false);
```