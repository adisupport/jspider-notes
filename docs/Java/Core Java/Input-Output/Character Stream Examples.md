# Read Line by Line

```Java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class ReadLineByLine {

  public static void main(String[] args) {
    // Replace "path/to/your/file.txt" with the actual file path
    String filePath = "path/to/your/file.txt";

    try (BufferedReader reader = new BufferedReader(new FileReader(filePath))) {
      String line;
      while ((line = reader.readLine()) != null) {
        // Process the line here
        System.out.println(line); // Example: Print each line
      }
    } catch (IOException e) {
      e.printStackTrace();
    }
  }
}

```

# Write into text file.
```Java
import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;
import java.util.Scanner;

public class StoreStudentInfo {

  public static void main(String[] args) {
    Scanner scanner = new Scanner(System.in);

    // Get student information from user
    System.out.print("Enter student name: ");
    String name = scanner.nextLine();
    System.out.print("Enter student ID: ");
    int id = scanner.nextInt();
    scanner.nextLine(); // Consume newline character after int input

    // Create student object (optional, for better organization)
    Student student = new Student(name, id);

    // Write student information to file
    String filePath = "students.txt"; // Replace with your desired file name
    writeStudentToFile(student, filePath);

    System.out.println("Student information stored successfully!");

    scanner.close();
  }

  public static void writeStudentToFile(Student student, String filePath) {
    try (BufferedWriter writer = new BufferedWriter(new FileWriter(filePath, true))) {
      writer.write(student.toString() + "\n"); // Write student info with newline
    } catch (IOException e) {
      e.printStackTrace();
      System.out.println("Error writing to file!");
    }
  }
}

// Optional class to represent Student object (can be modified)
class Student {
  private String name;
  private int id;

  public Student(String name, int id) {
    this.name = name;
    this.id = id;
  }

  @Override
  public String toString() {
    return name + "," + id; // Format student information for file storage (comma-separated)
  }
}

```

## Pipe Example

```Java
1. import java.io.PipedReader;  
2. import java.io.PipedWriter;  

4. public class PipeReaderExample2 {  
5.     public static void main(String[] args) {  
6.         try {  

8.             final PipedReader read = new PipedReader();  
9.             final PipedWriter write = new PipedWriter(read);  

11.             Thread readerThread = new Thread(new Runnable() {  
12.                 public void run() {  
13.                     try {  
14.                         int data = read.read();  
15.                         while (data != -1) {  
16.                             System.out.print((char) data);  
17.                             data = read.read();  
18.                         }  
19.                     } catch (Exception ex) {  
20.                     }  
21.                 }  
22.             });  

24.             Thread writerThread = new Thread(new Runnable() {  
25.                 public void run() {  
26.                     try {  
27.                         write.write("I love my country\n".toCharArray());  
28.                     } catch (Exception ex) {  
29.                     }  
30.                 }  
31.             });  

33.             readerThread.start();  
34.             writerThread.start();  

36.         } catch (Exception ex) {  
37.             System.out.println(ex.getMessage());  
38.         }  

40.     }  
41. }  

Output:

I love my country
```

