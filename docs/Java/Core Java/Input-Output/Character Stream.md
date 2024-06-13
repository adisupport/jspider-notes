
### Reader
```Java
abstract class Reader{
	int read();
	int read(char buffer[]);
	int read(char buffer[],int loc,int nChars);
	void mark(int nchars);
	void reset();
	long skip(long nChars);
	boolean ready();
	void close();
}
```

| SN  | Method                                       | Description                                                                                                                                                               |
| --- | -------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | int read()                                   | This method returns the integral representation of the next character present in the input. It returns -1 if the end of the input is encountered.                         |
| 2   | int read(char buffer[])                      | This method is used to read from the specified buffer. It returns the total number of characters successfully read. It returns -1 if the end of the input is encountered. |
| 3   | int read(char buffer[], int loc, int nChars) | This method is used to read the specified nChars from the buffer at the specified location. It returns the total number of characters successfully read.                  |
| 4   | void mark(int nchars)                        | This method is used to mark the current position in the input stream until nChars characters are read.                                                                    |
| 5   | void reset()                                 | This method is used to reset the input pointer to the previous set mark.                                                                                                  |
| 6   | long skip(long nChars)                       | This method is used to skip the specified nChars characters from the input stream and returns the number of characters skipped.                                           |
| 7   | boolean ready()                              | This method returns a boolean value true if the next request of input is ready. Otherwise, it returns false.                                                              |
| 8   | void close()                                 | This method is used to close the input stream. However, if the program attempts to access the input, it generates IOException.                                            |

### Reader Concrete Class

| SN  | Class                                                                        | Description                                                                                               | Popular Methods               |
| --- | ---------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- | ----------------------------- |
| 1.  | [BufferedReader](https://www.javatpoint.com/java-bufferedreader-class)       | This class provides methods to read characters from the buffer.                                           | .readLine()                   |
| 2.  | [CharArrayReader](https://www.javatpoint.com/java-chararrayreader-class)     | This class provides methods to read characters from the char array.                                       |                               |
| 3.  | [FileReader](https://www.javatpoint.com/java-filereader-class)               | This class provides methods to read characters from the file.                                             | .read(),         .available() |
| 4.  | [FilterReader](https://www.javatpoint.com/java-filterreader-class)           | This class provides methods to read characters from the underlying character input stream.                |                               |
| 5   | [InputStreamReader](https://www.javatpoint.com/java-inputstreamreader-class) | This class provides methods to convert bytes to characters.                                               |                               |
| 6   | [PipedReader](https://www.javatpoint.com/java-pipedreader-class)             | This class provides methods to read characters from the connected piped output stream.  Used With Threads | .connect(PipedWriter pw)      |
| 7   | [StringReader](https://www.javatpoint.com/java-stringreader-class)           | This class provides methods to read characters from a string.                                             |                               |
### Writer

```Java
abstract class Writer{
	private char[] writeBuffer;
	private static final int WRITE_BUFFER_SIZE = 1024;
	// to write the data to the output stream
	void write(); 
	// to write a single character to the output stream.
	void write(int i); 
	// to write the array of character to the output stream.
	void write(char buffer[]);
	//to write the nChars character to the character array from the specified location.
	void write(char buffer[],int loc,int nChars);
	// to close output stream.
	void close();
}
```

### Concrete Class Of Writer Class

| SN  | Class                                                                         | Description                                                                     | Practical Methods                         |
| --- | ----------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ----------------------------------------- |
| 1   | [BufferedWriter](https://www.javatpoint.com/java-bufferedwriter-class)        | This class provides methods to write characters to the buffer.                  | .newLine(),         .write(String s)      |
| 2   | [FileWriter](https://www.javatpoint.com/java-filewriter-class)                | This class provides methods to write characters to the file.                    | .write(char c),     .write(char[] c)      |
| 3   | [CharArrayWriter](https://www.javatpoint.com/java-chararraywriter-class)      | This class provides methods to write the characters to the character array.     | .writeTo(Writer w)                        |
| 4   | [OutpuStreamWriter](https://www.javatpoint.com/java-outputstreamwriter-class) | This class provides methods to convert from bytes to characters.                |                                           |
| 5   | [PipedWriter](https://www.javatpoint.com/java-pipedwriter-class)              | This class provides methods to write the characters to the piped output stream. | .connect(PipedReader pr),  .write(char c) |
| 6   | [StringWriter](https://www.javatpoint.com/java-stringwriter-class)            | This class provides methods to write the characters to the string.              |                                           |
| 7   | [PrintWriter](https://www.javatpoint.com/java-printwriter-class)              | provide print and println methods.                                              | .print(),                     .println()  |
