# Object Mapper

Sometime we require to read json and mapped to some java class.

we can easy do it with ObjectMapper provided by Jackson library.

```Java
public class Student{
	String name;
	int age;
}
//This json mapped to Student class
String jsonString = "{ \"name\": \"Alice\", \"age\": 30 }";

public class Main{
	public static void main(String args[]){
		ObjectMapper mapper = new ObjectMapper();
		Student student = mapper.readValue(jsonString,Student.class);
	}
}
```

Export class to Json string.
```Java
public Main{
	public static void main(String [] args){
		Student student = new Student("Alice",23);

		ObjectMapper mapper = new ObjectMapper();
		String json = mapper.writeValueAsString(student);
		System.out.println(json);
	}
}
```

# JWT

