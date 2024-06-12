How to think in java. 
- Java is [OOPs](LLD/OPPs) Based Programing Language. So, We Have to think in term of Objects and Classes.

- #### **Java is Passed By Value**,
	Java supports only call by value. So, if we pass a primitive value, it will not change the original value. But, if we convert the primitive value in an object, it will change the original value.
	
	> 	For ***Primitive Type*** Variables, Java is ***Passed by Value***
	> 	For ***Objects***, Java is Passed By ***Reference***
	
- #### **Deep Copy and Swallow Copy** 
	Because java is passed by Value, Coping an Object or Cloning it is bit tricky.
	To Learn More [Cloning of Object](Java/OPPs/Cloning).


- #### [Wrapper Classes](Wrapper Class) 
	to make primitive variable into objects.
	Why  Wrapper Class?
		- **Collection Framework:** Java collection framework works with objects only. All classes of the collection framework.
			1. [ArrayList](Java/Collection/List) (Dynamic Array)
			2. [LinkedList](Java/Collection/List) 
			3. [Vector](Java/Collection/List)
			4. [HashSet](Java/Collection/Set) (Binary Search Tree with implementation of Hashing)
			5. [HashMap](Java/Collection/Map)
			6. [TreeMap](Java/Collection/Map) 
			7. [TreeSet](Java/Collection/Set) (Binary Search Tree)
			8. [PriorityQueue](Java/Collection/Queue) (Heap)
			9. [Stack](Java/Collection/Stack)
			10. [Queue](Java/Collection/Queue)
		 deal with objects only.
		 - **Serialization:** We need to convert the objects into streams to perform the serialization. If we have a primitive value, we can convert it in objects through the wrapper classes.
		- **Synchronization:** Java synchronization works with objects in Multithreading.
		- **java.util package:** The java.util package provides the utility classes to deal with objects.

| Data Type | Wrapper Class |
| :---:| :--------------: |
| int | Integer|
| char | Character |
| bool | Boolean |
| float | Float |
| double | Double |

- #### **String Pool**  
	 Java has Concept of String Pools,

- #### Naming Convention :  
	Classes : Camel Case, it Should be Noun.
	Interfaces : Camel Case, it Should be adjective.
	methods and functions: Lowercase
	Variables : Lowercase
	Package : Lowercase
	Camel Case -  First letter of word will be capital.
		Example: EmployeeList

- #### [File Handling](Java/FileHandling)
- [Exception Handling](Java/Exception) 
- [Multithreading](Java/Multithreading)

