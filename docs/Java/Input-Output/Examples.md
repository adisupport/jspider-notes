### Store Student Info table format into file. 
```Java
public class StudentInfoWriter {

  public static void writeStudentInfoToFile(String fileName, String name, int age, String phoneNumber) throws IOException {
    String template = "+------------+-------+-------------+\n" +
                      "| Name       | Age  | Phone Number |\n" +
                      "+------------+-------+-------------+\n" +
                      "| %-10s | %3d  | %14s |\n" +
                      "+------------+-------+-------------+\n";

    String formattedInfo = String.format(template, name, age, phoneNumber);

    try (BufferedWriter writer = new BufferedWriter(new FileWriter(fileName, true))) {
      writer.write(formattedInfo);
    }
  }

  public static void main(String[] args) throws IOException {
    String fileName = "student_info.txt";
    String name = "John Doe";
    int age = 25;
    String phoneNumber = "123-456-7890";

    writeStudentInfoToFile(fileName, name, age, phoneNumber);
  }
}


```