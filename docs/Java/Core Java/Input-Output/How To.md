| SN  | How                                                                 | Article                                            |
| --- | ------------------------------------------------------------------- | -------------------------------------------------- |
| 1.  | How to read from file                                               | [[File Handling#Reading a file with Byte Stream]]  |
| 2.  | How to write into file                                              | [[File Handling#Write into file]]                  |
|     | How to append into text file                                        | [[#Append into text file]]                         |
| 3.  | How to Read Large File                                              | [[File Handling#Reading a Large file into chunks]] |
| 4.  | How to read line by line from text file                             |                                                    |
| 5.  | Store Object into File                                              | [[Byte Stream Application#Store Object Into File]] |
| 6.  | ObjectInputStream, Reading Object written using ObjectOutputStream. | [[Byte Stream Application#Reading All The Object]] |
| 7.  | Reading Compressed file                                             |                                                    |
| 8.  | Writing Compress File                                               |                                                    |
| 9.  | Encrypting a file.                                                  |                                                    |

## Append into text file
```Java
import java.io.BufferedWriter;
import java.io.FileWriter;
import java.util.Scanner;
  
public class AppendIntoFile {
    public static void main(String[] args) {
        try (BufferedWriter bw = new BufferedWriter(new FileWriter("buftext.txt",true))) {
            Scanner sc = new Scanner(System.in);
            int total = sc.nextInt();
            while((total--) != 0){
               String line = sc.nextLine();
               bw.write(line);
            }
            sc.close();
        } catch (Exception e) {
	        System.out.println(e.getMessage());
        }
    }
}
```