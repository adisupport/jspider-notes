
Byte Stream are defined by using two abstract class hierarchies.
- InputStream 
- OutputStream 
Each of these abstract classes has several concrete subclasses that handle the differences among various devices, such as disk files, network connections and even memory buffers.

### InputStream

```Java
abstract class InputStream{
	int read();
	int read(byte buffer[]);
	int read(byte buffer [],int loc,int nBytes);
	int available()
	void mark(int nBytes);
	void reset();
	long skip(long nBytes);
	void close(); 
}
```

| SN  | Method                                         | Description                                                                                                                                                                                                                            |
| --- | ---------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | int read()                                     | This method returns an integer, an integral representation of the next available byte of the input. The integer -1 is returned once the end of the input is encountered.                                                               |
| 2   | int read (byte buffer [])                      | This method is used to read the specified buffer length bytes from the input and returns the total number of bytes successfully read. It returns -1 once the end of the input is encountered.                                          |
| 3   | int read (byte buffer [], int loc, int nBytes) | This method is used to read the 'nBytes' bytes from the buffer starting at a specified location, 'loc'. It returns the total number of bytes successfully read from the input. It returns -1 once the end of the input is encountered. |
| 4   | int available ()                               | This method returns the number of bytes that are available to read.                                                                                                                                                                    |
| 5   | Void mark(int nBytes)                          | This method is used to mark the current position in the input stream until the specified nBytes are read.                                                                                                                              |
| 6   | void reset ()                                  | This method is used to reset the input pointer to the previously set mark.                                                                                                                                                             |
| 7   | long skip (long nBytes)                        | This method is used to skip the nBytes of the input stream and returns the total number of bytes that are skipped.                                                                                                                     |
| 8   | void close ()                                  | This method is used to close the input source. If an attempt is made to read even after the closing, IOException is thrown by the method.                                                                                              |


![[File Handling#Reading a file with Byte Stream]]


![[File Handling#Reading a Large file into chunks]]



### Input Stream Concrete Classes

![[Pasted image 20240315140345.png]]
- FileInputStream(String filepath) : Create file stream, used for Reading Files.
- DataInputStream(InputStream): Used for readUTF()
- ObjectInputStream(InputStream): Used to Read Serialized object.
- BufferedInputStream(new FileInputStream()) : Work efficiently with file & Socket.



| SN  | Class                                                                                                       | Description                                                                                                           |     |
| --- | ----------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- | --- |
| 1   | [BufferedInputStream](https://www.javatpoint.com/java-bufferedinputstream-class)                            | This class provides methods to read bytes from the buffer.                                                            |     |
| 2   | [ByteArrayInputStream](https://www.javatpoint.com/java-bytearrayinputstream-class)                          | This class provides methods to read bytes from the byte array.                                                        |     |
| 3   | [DataInputStream](https://www.javatpoint.com/java-datainputstream-class)                                    | This class provides methods to read Java primitive data types.                                                        |     |
| 4   | [FileInputStream](https://www.javatpoint.com/java-fileinputstream-class)                                    | This class provides methods to read bytes from a file.                                                                |     |
| 5   | [FilterInputStream](https://www.javatpoint.com/java-filterinputstream-class)                                | This class contains methods to read bytes from the other input streams, which are used as the primary source of data. |     |
| 6   | [ObjectInputStream](https://www.javatpoint.com/java-objectinputstream)                                      | This class provides methods to read objects.                                                                          |     |
| 7   | [PipedInputStream](https://www.javatpoint.com/PipedInputStream-and-PipedOutputStream-classes-using-threads) | This class provides methods to read from a piped output stream to which the piped input stream must be connected.     |     |
| 8   | [SequenceInputStream](https://www.javatpoint.com/java-sequenceinputstream-class)                            | This class provides methods to connect multiple Input Stream and read data from them.                                 |     |
|     |                                                                                                             |                                                                                                                       |     |
|     |                                                                                                             |                                                                                                                       |     |
|     |                                                                                                             |                                                                                                                       |     |
![[Pasted image 20240315210204.png]]

> [!note] Most Used Class
> 1. File Stream : ***FileInputStream*** and ***FileOutputStream***
> 2. Object Stream: ***ObjectInputStream*** and ***ObjectOutputStream***
> 3. Data Stream: **DataInputStream** and **DataOutputStream**


### OutputStream

```Java
abstract class OutputStream{
	void write(int i);
	void write(byte buffer[]);
	void write(byte buffer[],int loc,int nBytes);
	void flush();
	void close();	
}
```

| SN  | Method                                         | Description                                                                                                                                        |
| --- | ---------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | void write (int i)                             | This method is used to write the specified single byte to the output stream.                                                                       |
| 2   | void write (byte buffer [] )                   | It is used to write a byte array to the output stream.                                                                                             |
| 3   | Void write(bytes buffer[],int loc, int nBytes) | It is used to write nByte bytes to the output stream from the buffer starting at the specified location.                                           |
| 4   | void flush ()                                  | It is used to flush the output stream and writes the pending buffered bytes.                                                                       |
| 5   | void close ()                                  | It is used to close the output stream. However, if we try to close the already closed output stream, the IOException will be thrown by this method |
|     |                                                |                                                                                                                                                    |
### Output Stream Concrete Classes
![[Pasted image 20240315140322.png]]

| SN  | Class                                                                                                        | Description                                                         |
| --- | ------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------- |
| 1   | [BufferedOutputStream](https://www.javatpoint.com/java-bufferedoutputstream-class)                           | This class provides methods to write the bytes to the buffer.       |
| 2   | [ByteArrayOutputStream](https://www.javatpoint.com/java-bytearrayoutputstream-class)                         | This class provides methods to write bytes to the byte array.       |
| 3   | [DataOutputStream](https://www.javatpoint.com/java-dataoutputstream-class)                                   | This class provides methods to write the java primitive data types. |
| 4   | [FileOutputStream](https://www.javatpoint.com/java-fileoutputstream-class)                                   | This class provides methods to write bytes to a file.               |
| 5   | [FilterOutputStream](https://www.javatpoint.com/java-filteroutputstream-class)                               | This class provides methods to write to other output streams.       |
| 6   | ObjectOutputStream                                                                                           | This class provides methods to write objects.                       |
| 7   | [PipedOutputStream](https://www.javatpoint.com/PipedInputStream-and-PipedOutputStream-classes-using-threads) | It provides methods to write bytes to a piped output stream.        |
| 8   | [PrintStream](https://www.javatpoint.com/java-printstream-class)                                             | It provides methods to print Java primitive data types.             |
