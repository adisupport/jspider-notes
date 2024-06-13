Two of the most often-used stream classes are FileInputStream and FileOutputStream,which create bytes streams linked to files.

## Open a file

To Open a file, you simply create an object of one of these classes, specifying the name of the file as an argument to the constructor.

*FileInputStream(String filename)* throws FileNotFoundException
*FileOutputStream(String filename)* throws FileNotFoundException
*FileWriter(String filename)*
*FileReader(String filename)*

*filename* specifies the name of the file that you want to open.
When you create an input stream if the file does not exit, then FileNotFoundException is thrown.

For Ouput Streams, if the file cannot be opened or created, then FileNotFoundException is thrown.
When an output file is opened, any preexisting file by the same name is destroyed.

>[!note]
>In situations in which a security manager is present,several of file classes,including
> **FileInputStream** and **FileOutputStream**, will throw a SecurityException if a security violation occurs when attempting to open a file.
> In that case you need to handle this exception.

### Write into file

### Writing through byte stream
```Java
class FileWriter{
	public static void main(String args[]){
		try(OutputStream out = new FileOutputStream("out.txt")){
			byte arr[];
			byteArr = "Write these statement into file".getBytes();
			out.write(byteArr);
		}catch(Exception e){
			System.out.println(e.getMessage());
		}
		
	}
}
```

### Writing through character stream
```Java
class WriteIntoFile{
	public static void main(String args[]){
		try(Writer out = new FileWriter("out.txt")){
			out.write("Hello Java");
		}catch(Exception e){
			System.out.println(e.getMessage());
		}
		
	}
}
```
### Reading a file with Byte Stream

```Java
class Reader{
	public static void main(String [] args){
		try(InputStream in = new FileInputStream("in.txt")){
			int i;
			do{
				i = in.read();
				if(i != -1) System.out.println((char)i);
			}while(i != -1);
		}catch(FileNotFoundException e){
			System.out.println(e.getMessage());
		}
	}
}
```
.read() : read single byte.
### Reading a Large file into chunks
```Java
import java.io.*;
public class Example {
    public static void main(String[] args) {
        byte[] arr = new byte[1024];
        try (InputStream is = new FileInputStream("out3.txt")){
            int loop = 0;
            do {
                is.read(arr);
                for(int i=0;i<arr.length;i++){
                    System.out.print((char)arr[i]);
                }
                loop++;
            } while (loop!=2);
        } catch (Exception e) {
            System.err.println(e.getMessage());
        }
    }
}
```

> [!note]
> `byte[] arr = new byte[1024];` 
> `inputStream.read(arr)`: read upto size of arr,and store into arr.
> `inputStream.read(arr,offset,len):` read len byte from file and store at arr[offset];

### Can Wrap With BufferedInputStream
>[!warning]
>You may wonder every time you call read method this might read same data but that's not the case it has cursor that moves every time you called it. 
>

```Java
import java.io.*;
public class Example {
    public static void main(String[] args) {
        byte[] arr = new byte[1024];
        try (InputStream is = new BufferedInputStream(FileInputStream("out3.txt"))){
            int loop = 0;
            do {
                is.read(arr,loop*5,25);
                for(int i=0;i<arr.length;i++){
                    System.out.print((char)arr[i]);
                }
                loop++;
            } while (loop!=2);
        } catch (Exception e) {
            System.err.println(e.getMessage());
        }
    }
}
```
> [!note]
> `byte[] arr = new byte[1024]`
> `inputStream.read(arr,offset,len)`:  Read `len` bytes and store at `arr[offset]` to `arr[offset + len]` ;

# Random Access
