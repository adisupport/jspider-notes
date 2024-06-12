# Project Intro 

We are Building a Proxy server for [Fake Store API](https://fakestoreapi.com).

API Documentation: [Fake Store API](https://fakestoreapi.com/docs)

What is a Proxy Server?

Proxy Server is an intermediary Application Server Which  takes request from clients.
Validate it, Then make Call Behalf of Client and Send Response.

![Proxy Server Diagram](https://bytesofgigabytes.com/IMAGES/Networking/proxyserver/Proxy%20server.png)

#### FakeStore Routes
	we are Creating Proxy For these Routes.
	Product API: `https:fakestoreapi/products`

# Setup Spring Project

How to Setup Spring Boot Project? Read this [Spring | Quickstart](https://spring.io/quickstart/) 
Necessary Dependency
`1. Spring Web
`2. Lombok`

Package Manager `Maven`
Project Name `FakeStoreProxy`

Open Project File in your IDE,I am using Intelij IDE.

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
# Schema/Models
1. Product
2. Rating
3. Category


1. Product Model
``` Java 
@Getter  
@Setter  
public class Product {  
    Long id;  
    String title;
    String description;
    Category category;    
    Double price;
    String imageUrl;  
    Rating rating;  
}
```
2. Rating Model
``` Java
@Getter  
@Setter  
public class Rating {  
    Float rate;  
    Integer count;  
}
```
3. Category Model
``` Java
@Getter  
@Setter  
public class Category {  
    String name;  
    public Category(String category) {  
        this.name = category;  
    }  
}
```


# Data Transfer Object

What is Data Transfer Object (DTO) it's a class that used for one - one mapping to the Response we are receiving from Web(Request, Response of Http Clients).
It more Like converting JSON response into Java Class Entity,
where every properties of JSON is the Attribute of the Class, This class is Called DTO.


JSON Response from `https:fakestoreapi/products/1`  route.
``` javascript 
{ 
id:1, 
title:'...', 
price:'...', 
category:'...',
description:'...', 
image:'...',
rating:{
		count:'...',
		rate:'...'
	}
}
```


DTO Class for `Product route` response 

``` Java
@Setter  
@Getter  
public class FakeStoreProductDTO {  
    Long id;  
    String title;  
    Double price;  
    String category;  
    String Description;  
    String image;  
    Rating rating;  
}
```

**Spring use JACKSON  to maps JSON to DTO class.
`Note: I missed to put annotation of @Getter and @Setter in Rating Class.Spring Boot than throws Can't have one-one mapping error.` **DON'T FORGET EVER**


# Controllers

ProductsController

``` JAVA
package com.zoomcar.fakestoreproxy.controllers;  
  
import org.springframework.beans.factory.annotation.Autowired;  
import org.springframework.web.bind.annotation.*;  
import org.springframework.web.client.RestTemplate;  
  
import java.util.List;  
  
@RestController  
@RequestMapping("/products")  
public class ProductController {  
  
    ProductServices productService;  
    @Autowired  
    public ProductController(ProductServices productService){  
        this.productService = productService;  
    }    
}
```
