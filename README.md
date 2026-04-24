# java




public class Knapsack01 {
    public static int knapsack(int[] wt, int[] val, int W, int n) {
        int[][] dp = new int[n + 1][W + 1];

        for (int i = 0; i <= n; i++) {
            for (int w = 0; w <= W; w++) {

                if (i == 0 || w == 0) {
                    dp[i][w] = 0;
                } 
                else if (wt[i - 1] <= w) {
                    dp[i][w] = Math.max(
                        val[i - 1] + dp[i - 1][w - wt[i - 1]],
                        dp[i - 1][w]
                    );
                } 
                else {
                    dp[i][w] = dp[i - 1][w];
                }
            }
        }
        return dp[n][W];
    }

    public static void main(String[] args) {
        int[] wt = {1, 3, 4, 5};
        int[] val = {1, 4, 5, 7};
        int W = 7;
        int n = wt.length;

        System.out.println(knapsack(wt, val, W, n));
    }
}





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