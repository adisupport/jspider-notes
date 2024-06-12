### What is Socket?
A **socket** is one endpoint of a **two way** communication link between two programs running on the network. The socket mechanism provides a means of inter-process communication (IPC) by establishing named contact points between which the communication take place.

Socket in act as identifier for OS to redirect incoming network request and response to particular application.

![[Connection diagram.png]] In This Figure we can see structure of computer networks.

Router allocated address to all the computer that are connected with it.
This address is called IP address.

If a process want to send a data to other process it either to same computer or different how we do it?
answer is Sockets!,
Socket is mechanism that provided by OS to communicate other Process.

How Sockets Works?
There are Two Types of Sockets
1. Connection-oriented ( TCP protocols )
2. Connectionless ( UDP protocols  )
### Connection oriented Sockets 

![[TCP diagram.jpg]]
Server: There Process who receive request and then response.
Client: Process which request and get response back.

# CREATING  SERVER IN  JAVA
Library that provide classes of Socket is in `java.net.*`
`import java.net.*`

```Java
package Networking;

import java.io.DataOutputStream;
import java.io.IOException;
import java.net.ServerSocket;
import java.net.Socket;
  
public class Server {
    public Server(){
        try{
		    int port = 6666;
            ServerSocket server = new ServerSocket(port);
            Socket clientSocket;
            System.out.println("Server is Running at " + port);
            while(!server.isClosed()){
                System.out.println("Waiting for Client");
                clientSocket = server.accept();
                clientAddress = clientSocket.getInetAddress();  
                System.out.println("Client "+ clientAddress + "is Connected");    

                DataOutputStream outputStream = new 
                DataOutputStream(clientSocket.getOutputStream());
                outputStream.writeUTF("HELLO");

				//Client Connection closed
                clientSocket.close();
            }
            server.close();
        }catch(IOException e){
            System.out.println(e);
        }
    }
    public static void main(String[] args) {
        new Server();
    }
}
```

# Creating CLIENT

```Java
package Networking;
import java.net.*;
import java.io.*;

public class Client{
    public static void main(String[] args ) {
        try {
            // Requesting Connection 
            Socket s = new Socket("localhost",6666);  
            
            //InputStream
            DataInputStream din=new DataInputStream(s.getInputStream());
            System.out.println(din.readUTF());  
            
            s.close();
        } catch (Exception e) {
            System.out.println(e.getMessage());
        }
    }
}
```