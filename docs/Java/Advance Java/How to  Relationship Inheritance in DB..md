
#### Overview


###Schema
![[WhatsApp Image 2024-01-25 at 18.39.22_3e975a25.jpg]]


```Java
class User{
	String name;
	String email;
	String password;
}
class Instructor extends User{
	String specialization;
}
class Mentor extends User{
	String company;
	double avgRating;
} 
class TA extends User{
	int noOfSessions;
	double avgRating;
} 
class Student extends User{
	int Batch;
	String Course;
}
```
---
# How to store in DB?

These are the 4 Ways
1. [[#<center><h1 id="MapSuperClass">Map Super Class</h1></center>]]
2. [[#TablePerClass]]
3. [[#Joined Table [Most Used Way]]]
4. [[#SingleTabl]]

---
# Joined Table [Most Used Way]
Every data with respect to objects of parent classs, i will have in the parent table.
For each child class also create a table with only with it's own attribute.
parent class attribute access via foreign key.

![[Pasted image 20240125210854.png]]




#### Code
```Java
@Entity
@Inheritance(strategy = InheritanceType.Joined)
class User{
	@Id
	Long id;
	String name;
	String email;
	String password;
}

@Entity
@PrimaryKeyJoinColumn(name = "user_id")
class Instructor extends User{
	String specialization;
}

@Entity
@PrimaryKeyJoinColumn(name = "user_id")
class Mentor extends User{
	String company;
	double avgRating;
} 

@Entity
@PrimaryKeyJoinColumn(name = "user_id")
class TA extends User{
	int noOfSessions;
	double avgRating;
} 


@Entity
@PrimaryKeyJoinColumn(name = "user_id")
class Student extends User{
	int Batch;
	String Course;
}

```
---
# Map Super Class



![[Pasted image 20240125190203.png]]


> DB Snapshot
>
![[Pasted image 20240125205748.png]] 

>[!note] Point To Remember
>1. This strategy should use in when parent is abstract class or object/table of Parent class is not required. 
>
>2. Table will created only for child class.
>3. Read this for how to setup [[Model]].
> 4. Mark Parent model with `@MappedSuperClass` annotation.
>

<center>User Model</center>
```Java
@Entity
@MappedSuperClass
class User{
	String name;
	String email;
	String password;
}

@Entity
class Instructor extends User{
	String specialization;
}

@Entity
class Mentor extends User{
	String company;
	double avgRating;
} 

@Entity
class TA extends User{
	int noOfSessions;
	double avgRating;
}

@Entity
class Students extends User{
	String Course
	int Batch;
}

```




# Table Per Class

![[Pasted image 20240125205919.png]]
Same as Mapped Supper Class But Table of Parent Class also Created.











# Single Table

![[Pasted image 20240125205031.png]]


```Java
@Getter
@Setter
@Entity
@Inheritance(strategy = InheritanceType.SINGLE_TABLE)  
@DiscriminatorColumn(  
        name = "user_type",  
        discriminatorType = DiscriminatorType.INTEGER  
)  
@DiscriminatorValue(value = "0")
class User{
	String name;
	String email;
	String password;
}
```

<center>Instructor Model</center>
```Java
@Getter
@Setter
@Entity
@DiscriminatorValue(value = "2")
class Instructor extends User{
	String specialization;
}
```
<center>Mentor Model</center>
```Java
@Getter
@Setter
@Entity
@DiscriminatorValue(value = "1")
class Mentor extends User{
	String company;
	double avgRating;
} 
```

<center>TA Model</center>
```Java
@Getter
@Setter
@Entity
@DiscriminatorValue(value = "3")
class TA extends User{
	int noOfSessions;
	double avgRating;
}
```

<center>Student Model</center>
```Java
@Getter
@Setter
@Entity
@DiscriminatorValue(value = "4")
class Student extends User{
	int Batch;
	String Course;
}
```


> [!tip] Annotation Brief
> 1. @Entity : Mark class as entity, To tell spring to create table in DB.
> ```
> @Entity
> class User{
> 	Long id;
> 	String name;
> } 
>```
>2. A table will created with name as users and column as attribute of class.
>
>
>
>2. @Entity(name = "users") for specify custom table name.
> 
>2. @Inheritance(strategy = InheritanceType): This Annotation used for set Inhetitance Repesentation.
>### InheritanceType
>1. SINGLE_TABLE (default)
>2. TABLE_PER_CLASS
>3. JOINED
>
>Use Inheritance Annotation for Parent Model ONLY.


> [!note] Annotation
> 1. `@Inheritance(strategy = InheritanceType.SINGLE_TABLE)`: Set Inheritance Strategy 
> 2. `@DiscriminatorColumn(name, discriminatorType)`: 
> In Single Table we add column to identify this row belong to which entity(User,Mentor,Instructor,TA or Students).
> 0-> User 
> 1 -> Mentor
> 2 -> Instructor
> 3 -> TA
> 4 -> Students
> 3. `@DiscriminatorValue(0)`: to assign models value which fill in `user_type` column.