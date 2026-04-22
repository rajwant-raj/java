# java


```

// Client.java
import java.io.*;
import java.net.*;

public class Client {
    public static void main(String[] args) {
        try {
            // Connect to server (localhost, port 5000)
            Socket socket = new Socket("localhost", 5000);

            // Receive data from server
            DataInputStream dis = new DataInputStream(socket.getInputStream());
            String serverTime = dis.readUTF();

            // Print received message
            System.out.println(serverTime);

            // Close connection
            socket.close();

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```



```

// Server.java
import java.io.*;
import java.net.*;
import java.util.Date;

public class Server {
    public static void main(String[] args) {
        try {
            // Create server socket on port 5000
            ServerSocket serverSocket = new ServerSocket(5000);
            System.out.println("Server started. Waiting for the client...");

            // Accept client connection
            Socket socket = serverSocket.accept();
            System.out.println("Client connected");

            // Send date and time to client
            DataOutputStream dos = new DataOutputStream(socket.getOutputStream());
            Date date = new Date();
            dos.writeUTF("Server Date and Time: " + date.toString());

            // Close connections
            socket.close();
            serverSocket.close();

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}


```