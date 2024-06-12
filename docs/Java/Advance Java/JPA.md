Java Persistence API is framework for handling Database.
The beauty of JPA is its reduce all the complex code to execute SQL query.

How it do?
<center><h3>Product Table</h3></center>

| id | name | description | image | price |
| :--- | :--- | ---- | ---- | ---- |
| 1 | Dell Laptop | intel i5 processor,8Gb RAM | url | 63k |
| 2 | HP Laptop | intel i5 processor,8Gb RAM | url | 57k |
| 3 | Acer Laptop | intel i5 processor,8Gb RAM | url | 45k |
Suppose, You want list of all laptop in product table how we will do it.
>[!note] Without JPA
>This will we SQL Query
>```Java
> String query = "Select product_name from Product where product_name like %laptop%;"
>```
>Now we have to use JDBC to execute this query. 
>1. Where first setup driver,
>2. create connection,
>3. create DB cursor,
>4. then execute query,
> 5. then convert  output ResultSet required to service layer.
> ---
> ### Read this article for how to use [[JDBC#5 Step To Run SQL Query On Database Using JDBC.]] 

---
> [!note] With JPA
> ```Java
> public interface ProductRepository extends Repository<Product,Long>{
> 	`public List<Product> findByNameLike(String like);`	
> }
> ```
>That's it JPA will parse the query method name inside ProductRepository interface and generate SQL query accordingly and all implementation is handled by ORM.
>[[#How To Write Method Name]]

---
# JPA Setup 
> [!note] JPA Setup
> First we have to add this value in `application.properties` file
> ``` Java
> spring.jpa.hibernate.ddl-auto=update  
>spring.datasource.url=jdbc:mysql://localhost/fakestore  
>spring.datasource.username=root  
>spring.datasource.password=admin  
>spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver  
>spring.jpa.show-sql: true
> ```
> *hibernate.ddl-auto*: To allow hibernate to modify table schema,
> 	OPTIONS -> [create,update,none,validate,drop-create]
> *spring.datasource.driver-class-name*: package name of Driver.
> 
|Database | Driver Class name|
>|:---:|:----:|
>|MySQL|  	com.mysql.cj.jdbc.Driver|
>|Postgres| org.postgresql.Driver|
 	
---
### Adding Dependencies 
Add these package into pom.xml

> Spring-Data-JPA 
```xml
<dependency>  
    <groupId>org.springframework.boot</groupId>  
    <artifactId>spring-boot-starter-data-jpa</artifactId>  
</dependency>
```

| Database Driver Package
> MySQL Driver

```xml
<dependency>  
    <groupId>com.mysql</groupId>  
    <artifactId>mysql-connector-j</artifactId>  
    <scope>runtime</scope>  
</dependency>
```

Postgres Driver
```xml
<dependency>  
    <groupId>org.postgresql</groupId>  
    <artifactId>postgresql</artifactId>  
    <scope>runtime</scope>  
</dependency>

```
# How To Write  Query Method Name

