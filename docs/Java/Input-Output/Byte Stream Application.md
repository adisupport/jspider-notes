
### 1. Reading a image file

```Java
import java.io.FileInputStream;

public class ReadImage {
    public static void main(String[] args) throws Exception {
        FileInputStream imageStream = new FileInputStream("image.jpg");

        // Read bytes from the image file
        byte[] imageData = new byte[imageStream.available()];
        imageStream.read(imageData);

        // Process the image data (e.g., display, compress)

        imageStream.close();
    }
}

```

### 2.Writing a compressed Archive

```Java
import java.io.FileOutputStream;
import java.util.zip.GZIPOutputStream;

public class CreateArchive {
    public static void main(String[] args) throws Exception {
        FileOutputStream fileStream = new FileOutputStream("archive.gz");
        GZIPOutputStream archiveStream = new GZIPOutputStream(fileStream);

        // Compress and write data to the archive (replace with your data)
        String dataToCompress = "This is some data to compress.";
        archiveStream.write(dataToCompress.getBytes());

        archiveStream.close();
        fileStream.close();
    }
}

```

## Base64 Encoding 
```Java
import java.util.Base64;

String data = "This is some binary data.";
byte[] bytes = data.getBytes();

// Encode
String encodedString = Base64.getEncoder().encodeToString(bytes);

// Decode
byte[] decodedBytes = Base64.getDecoder().decode(encodedString);
String decodedData = new String(decodedBytes);

```


# Store Object Into File

- to persistent of class object is called serialization and deserialization of object.
- to achieve that we first have to implement Serializable

```Java
import java.io.*;
import java.util.*;

class Student implements Serializable{
    String name;
    int age;
    public Student(String name,int age){
        this.name = name;
        this.age = age;
    }
    @Override
    public String toString() {
        return "{"+name+", "+age+"},";
    }
}

class Batch implements Serializable{
    int id;
    List<Student>students;    
    int noOfStudents;
    public Batch(){
        Random random = new Random();
        id = random.nextInt();
        students = new ArrayList<Student>();
    }
    public void addStudents(Student student){
        students.add(student);
    }
    @Override
    public String toString() {
        StringBuilder stringBuilder = new StringBuilder();
        stringBuilder.append(id+": ");
        stringBuilder.append("{");
        for (Student student : students) {
            stringBuilder.append(student.toString());
        }
        stringBuilder.append("}, ");
        return stringBuilder.toString();
    }
}


```

### Writing Student and Batch Object into `obj` file

```Java
public class WritingObject {
    public static void main(String[] args) {
        try (ObjectOutputStream os = new ObjectOutputStream(new FileOutputStream("obj"))) {
            Batch batch = new Batch();
            Student s1 = new Student("amit",18);
            Student s2 = new Student("arpit",20);
            batch.addStudents(s1);
            batch.addStudents(s2);

            os.writeObject(batch);
            // Write Object in obj.txt
            os.writeObject(s1);
            os.writeObject(s2);
            os.writeInt(0);
        } catch (Exception e) {
            System.out.println(e.getMessage());
        }
    }
}
```

# Reading Objects

```Java
import java.io.*;
public class ReadingObject {
    public static void main(String[] args) {
        try (ObjectInputStream ois = new ObjectInputStream(new FileInputStream("obj"))) {
            // Batch batch = (Batch)ois.readObject();
            Object object = null;
            while((object = ois.readObject())!= null){
	            System.out.println(object);
	        }
        } catch (Exception e) {
            System.out.println(e.getMessage());
        }
    }
}
```

# PrintStream
```Java
import java.io.*;
import java.util.Scanner;

public class CharacterStream {
    public static void main(String[] args) {
        try(Writer out = new FileWriter("out4.txt")){
            Scanner sc = new Scanner(System.in);
            PrintWriter pw = new PrintWriter(out);

            pw.append("----------------\n");
            int line = sc.nextInt();

            pw.format("{Total Number of line %s}", line);

            while((line--)!=-1){
                pw.println(sc.nextLine());
            }
            pw.append("----------------");
            sc.close();
        }catch(Exception e){
            System.out.println(e);
        }
    }
}
```

