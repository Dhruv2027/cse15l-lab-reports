# Lab Report 2
***
# Part 1
```java
import java.io.IOException;
import java.net.URI;
import java.util.*;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    // int num = 0;
    ArrayList<String> string = new ArrayList<>();
    ArrayList<String> name = new ArrayList<>();
    String script = "";

    public String handleRequest(URI url) {
        if (url.getPath().contains("/add")) {
            String[] parameters = url.getQuery().split("&");
            script += parameters[1].split("=")[1] + ": "+ parameters[0].split("=")[1] + '\n';
            return script;
        }
    
        return "404 Not Found!";
    }
}

class ChatServer {
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
In the code, I am storing whatever is added in the query part of the URL in the 

***
# Part 2
In the screenshot below, I have used the command `ssh-keygen` to create a public/private key pair. 

![Image](SS1.png)

As can be seen in the screenshot, my private key has been saved in the path `/Users/dhruvsharma/.ssh/id_rsa` and my public key has been saved in the path `/Users/dhruvsharma/.ssh/id_rsa.pub`. This means that the keys are stored in a folder named `.ssh` with the path `/Users/dhruvsharma/.ssh`.

![Image](SS2.png)

While on my local terminal, I, using the `scp` command, I securely copied my `id_rsa.pub` key into the `~/.ssh/authorized_keys` folder in `ieng6`. Next, I just entered the regular command to ssh into the `ieng6` account, `ssh d4sharma@ieng6.ucsd.edu`. As can be seen, I did not need to enter the password in this interaction. 
***
# Part 3
Over the past few weeks, I learnt how to connect to a server using `ssh`. I had heard of the term `ssh` but had no idea what it did. After coming into the class I realised exactly what each of the commands do and how the terminal works (atleast on a surface level). Over the last couple of weeks I also learnt aboout how websites can be created and watch its contents change using java by writing commands in the URL. These concepts are very new to me, so was a good learning opportunity. Furthermore, I learnt about URL and its specific parts. The only part I knew prior to the course was the domain, but now I can see that there are many parts to the URL like the query, anchor, etc. I also did not realise that the URL itself was a kind of path to the content we want to view.
