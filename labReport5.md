# CSE 15L lab report 5
---

## Part 1: Debugging Scenario

**Context:**
Student Name - Kay

TA - Gio

Directory Structure:
```
PA15/
    └── wavelet/
            ├── NumberServer.java
            ├── Server.java
            └── runServer.sh
Credit to Chat GPT for a copy and paste for this structure
```

Inside `NumberServer.java`: 
```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    int num = 0;

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format("Number: %d", num);
        } else if (url.getPath() == ("/increment")) {
            num += 1;
            return String.format("Number incremented!");
        } else {
            if (url.getPath().contains("/add")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("count")) {
                    num += Integer.parseInt(parameters[1]);
                    return String.format("Number increased by %s! It's now %d", parameters[1], num);
                }
            }
            return "404 Not Found!";
        }
    }
}

class NumberServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```

Inside `Server.java`:
```
// A simple web server using Java's built-in HttpServer

// Examples from https://dzone.com/articles/simple-http-server-in-java were useful references

import java.io.IOException;
import java.io.OutputStream;
import java.net.InetSocketAddress;
import java.net.URI;

import com.sun.net.httpserver.HttpExchange;
import com.sun.net.httpserver.HttpHandler;
import com.sun.net.httpserver.HttpServer;

interface URLHandler {
    String handleRequest(URI url);
}

class ServerHttpHandler implements HttpHandler {
    URLHandler handler;
    ServerHttpHandler(URLHandler handler) {
      this.handler = handler;
    }
    public void handle(final HttpExchange exchange) throws IOException {
        // form return body after being handled by program
        try {
            String ret = handler.handleRequest(exchange.getRequestURI());
            // form the return string and write it on the browser
            exchange.sendResponseHeaders(200, ret.getBytes().length);
            OutputStream os = exchange.getResponseBody();
            os.write(ret.getBytes());
            os.close();
        } catch(Exception e) {
            String response = e.toString();
            exchange.sendResponseHeaders(500, response.getBytes().length);
            OutputStream os = exchange.getResponseBody();
            os.write(response.getBytes());
            os.close();
        }
    }
}

public class Server {
    public static void start(int port, URLHandler handler) throws IOException {
        HttpServer server = HttpServer.create(new InetSocketAddress(port), 0);

        //create request entrypoint
        server.createContext("/", new ServerHttpHandler(handler));

        //start the server
        server.start();
        System.out.println("Server Started!");
    }
}
```

Inside `runServer.sh`:
```
javac *.java

java NumberServer $1
```
## Subject of Post: PA 15: Introduction to URL's and Serversn (actually week 2/3 clone) (Focus on java file Help)


Kay - 
> Hi, I currently have an issue with my code. Though it compile and runs, with the server starting successfully, the issue I come across is that when I add `/increment` to the end of the URL, I am expecting for the `num` variable to increment by one, and text to appear saying that it incremented. However, when I type `/increment` to the end of the URL, I notice that i just get an error saying "404 Not Found!". If it also helps, I am also running the server using the bash file, with the command `bash runServer.sh 4000`. 

> Here are some screenshots of the issue:
![img1.png](img1.png)
![img2.png](img2.png)
![img3.png](img3.png)

> My original assumption is that it had something to do with the return statement and where it was placed, but looking through the indentation, I dont believe as that is the case as it comes after the `/increment` statement. 

Gio - 
> Hi Kay! Your NumberServer.java code looks well done!, however I did notice an error. Have you looked into what determines if the argument is equal to `/increment` or not? Consider the value `/increment` is being compared to.
Kay-
> ohhhh, I think I understand now, since in my code i used `==`, which is used only for values of equal type, instead I should of used `.equals()`. Thanks for the help!

Fixed `NumberServer.java`:
```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    int num = 0;

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format("Number: %d", num);
        } else if (url.getPath() == "/increment") {
            num += 1;
            return String.format("Number incremented!");
        } else {
            if (url.getPath().contains("/add")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("count")) {
                    num += Integer.parseInt(parameters[1]);
                    return String.format("Number increased by %s! It's now %d", parameters[1], num);
                }
            }
            return "404 Not Found!";
        }
    }
}

class NumberServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```
Output Now: 
![img4.png](img4.png)
![img5.png](img5.png)

## Subject of Post: PA 17: Bash Files (grade.sh clone)
Student Name - Kya

TA - Gio

Same structure as earlier, instead replace `runServer.sh` w/ `printContents.sh`.
Contents of the `printContents.sh`.
```
javac *.java

java NumberServer 4000 

curl -s http://localhost:4000/increment

curl -s http://localhost:4000 > output.txt

echo output.txt
```

Kya - 
> Hi! I am currently having issues with my bash file. The purpose of this file is to run the server, and run the `/increment` of the `NumberServer`. However, it did not run either. I speculate that it likely stopped at the 2nd command being `java NumberServer 4000` because it did compile and start the server. However, I do not know what to do with that info. How should I make it run the next commands? I attached the output of the bash below:
![img6.png](img6.png)

Gio - 
> Hi Kya, your idea is spot on! You should look through your notes and figure out how to make it run the future commands. A small hint is that its a single character!

Kya - 
> That did work, but now it doesnt echo the output.. but instead it outputs the title of the created file... "output.txt". Why is that?

Gio - 
> Remember what echo does, is there a better suited command for what you are trying to do?

Kya - 
> Ohhhh I remember now, grep exists... ill use that... thank you!

Output: 
![img7.png](img7.png)

New bash code:
```
javac *.java

java NumberServer 4000 &

curl -s http://localhost:4000/increment

curl -s http://localhost:4000/ > output.txt

grep output.txt
```

## Part 2:
In this class, and from the labs, I learned a lot. I learned how to use bash, which is something I have been wanting to do for a good while now. On top of that, I also learned to start a server and learned a bit about ports.
