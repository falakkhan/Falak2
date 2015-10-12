# Falak2
import java.net.*;
import java.util.Scanner;
import java.io.*;
/**
 * @author lycog
 */
public class TCPClient {
  public static void main(String[] args){
    try{
      Socket socket = new Socket("127.0.0.1", 8888);
      //Define read/write from socket
      PrintWriter out = new PrintWriter(socket.getOutputStream(), true);
      BufferedReader in =
              new BufferedReader(
                        new InputStreamReader(socket.getInputStream()));
 
      //Send hello message
      System.out.println("Enter ur number greater than 1:");
      Scanner sc = new Scanner(System.in);
      int i = sc.nextInt();
      String msg=null;
      out.println(i);
 
      //Receive a reversed message
      msg = in.readLine();
      System.out.println("Server : " + msg);
    }catch(IOException ioe){
      ioe.printStackTrace();
    }
  }
}









import java.io.*;
import java.net.*;
/**
 * @author lycog
 */
public class TCPServer {
  public static void main(String[] args){
    try{
      //Create server socket listening on port 8888
      ServerSocket server = new ServerSocket(8888);
 
      while(true){
        System.out.println("Waiting for client to connect...");
        Socket socket = server.accept();
 
        //Create read/write from socket
        PrintWriter out = new PrintWriter(socket.getOutputStream(), true);
        BufferedReader in =
                new BufferedReader(
                          new InputStreamReader(socket.getInputStream()));
 
        //client address
        InetAddress remoteIp = socket.getInetAddress();
 
        //Receiving from client
        String msg = in.readLine();
        //System.out.println("Client " + remoteIp + " : " + msg);
        int num=Integer.parseInt(msg);
        boolean result=isprime(num);
        if(result==true){
        	msg="Yes, the number is prime.";
        }
        else{
        	msg="No, its not prime.";
        }
        out.println(msg);
      }
    }catch(IOException ioe){
      ioe.printStackTrace();
    }
  }
 
  private static boolean isprime(int num) {
	// TODO Auto-generated method stub
	  for(int i=2; i<=num/2; i++){

          if(num % i == 0){

              return false;

          }

      }

	return true;
}


}
