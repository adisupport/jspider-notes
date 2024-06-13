A stream is an abstraction that either produces or consumes information.
- Stream is linked to a physical device by the Java I/O system.
- Java Uses Stream to deal with Input/Output.
- Stream provide abstract to deal with different kind of devices,it means an input stream can abstract many different kinds of input:
	- from a console,
	- a disk file
	- keyword
	- or a network socket.
- Likewise Output stream may refer to the console,a disk file, or a network connection.
- Java implements Stream within Class hierarchies defined in the java.io packages.


![[Pasted image 20240315135327.png]]
 
> [!notes]
> Remember, to use the stream classes, you must import **Java.io**.
# Byte Stream & Character Streams


![[Pasted image 20240314181956.png]]
Java defines two types of streams
- [[Byte Stream]] : When handling reading or writing of binary data.
	- Designed for working with raw binary data (images, audio, video, compresses files, etc...).
	- Operate on data in units of 8-bit bytes.
	- Don't handle character encoding. You need to manage encoding/decoding if necessary.
	- Example of classes:
		- FileInputStream :Reads Bytes from a file.
		- FileOutputStream: Writes bytes to a file.
		- BufferedInputStream: Reads bytes efficiently from a byte stream (often used with FileInputStream) 
		- BufferedOutputStream: Writes bytes effieciently to a byte stream (often used with FileOutputStream)
- [[Character Stream]] : When handling reading or writing of character
	- Designed for working with text data (letters, digits, symbols).
	- Operate on data in units of 16-bit characters (typically using unicode encoding).
	- Handle character encoding automatically, converting between bytes an characters based on the system's default encoding(often UTF-8).
	- Example of classes:
		- FileReader: Reads characters from a text file.
		- FileWriter: Writes characters to a text file.
		- BufferedReader: Reads characters efficiently from a character stream (often used with FileReader).
		- BufferedWriter: Writes characters efficiently to a character stream(often used with FileWriter).
### When to Use Which:
- Use Character streams for working with text files where you want to read/write human-readable characters.
- Use byte streams for working with any type of binary data where you need to handle the data at a byte level or don't need to interpret it as characters.

| Feature      | Character Stream               | Byte Stream                                 |
| ------------ | ------------------------------ | ------------------------------------------- |
| Data Unit    | 16-bit Character(Unicode)      | 8-bit                                       |
| Encoding     | Handles encoding automatically | Requires manual encoding/decoding           |
| Suitable for | Text files                     | Binary files(images, audio, etc).           |
| Classes      | `FileReader`,`FileWriter`,etc. | `FileInputStream`, `FileOutputStream`, etc. |

