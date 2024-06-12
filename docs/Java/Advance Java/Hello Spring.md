# Setup Spring Project

How to Setup Spring Boot Project? Read this [Spring | Quickstart](https://spring.io/quickstart/) 
Necessary Dependency
`1. Spring Web

Package Manager `Maven`

# Hello Spring  
``` JAVA
@RestController
@RequestMapping("/hello")
public class HelloController{
	@GetMapping() 
	public String sayHello(){
		return "Hello SPRING"
	}
}
```

This is the bare minimum code start spring server of Hello.

| Annotations | Descriptions |
| :--: | :--- |
| @RestController | In Spring Controllers are the Routes or API ENDPOINTS.This annotation marks HelloController class as Controller |
| @RequestMapping("/hello") | HelloController class mapped to `http://localhost:8080/hello` but when you hit this API then nothing happens because we don't map HTTP Methods yet. |
| @GetMapping() | This Annotation Map the Get HTTP Methods, When we hit get request on `http://localhost:8080/hello` we get `Hello SPRING` in Response. |

# Variable Path Controller

`https://localhost:8080/hello/Adi`
OUTPUT: `HELLO Adi`

``` JAVA
@RestController
@RequestMapping("/hello")
public class HelloController{
	@GetMapping("/{name}") 
	public String sayHello(@PathVariable("name") String name){
		return "Hello " + name;
	}
}
```

# Take Input From Params/Queries 

`https://localhost:8080/hello?name=Adi`
OUTPUT: `HELLO Adi`

Method 1: Generic Method
``` JAVA
@RestController
@RequestMapping("/hello")
public class HelloController{
	@GetMapping() 
	public String sayHello(@RequestParams Map<String,String> params){
		return "Hello" + params.get("name");
	}
}
```

Method 2 : Specific Method

``` JAVA
@RestController
@RequestMapping("/hello")
public class HelloController{
	@GetMapping() 
	public String sayHello(@RequestParams(value = "name", required = true) String name){
		return "Hello" + name;
	}
}
```