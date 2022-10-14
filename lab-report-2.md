---
layout: post
title: Web Servers and Debugging
---

## Part One: Web Servers
For this part, I hosted a web server on ieng6 by running the following commands:
```
ssh cs15lfa22aq@ieng6.ucsd.edu
javac Server.java SearchEngine.java
java SearchEngine [port]
```
If I'm on ieng6-201, I can go to http://ieng6-201.ucsd.edu:9530/ to access my web server.

Note: It doesn't work if you aren't connected to UCSD-Protected or RESNET - Protected. There's a UCSD VPN that we otherwise.

 Below is the code for my simple search engine (also available in [this](https://github.com/kalkulator413/wavelet) github repo):
```
import java.io.IOException;
import java.net.URI;
import java.util.HashSet;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    HashSet<String> words = new HashSet<>();

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format("Welcome to my amazing search engine 8)\nGo to /add?s={word}" 
                + "to add a word\nUse /search?s={str} to return all words that contain str");
        } else {
            // System.out.println("Path: " + url.getPath());
            if (url.getPath().contains("/add")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    if (!words.contains(parameters[1])) {
                        words.add(parameters[1]);
                        return String.format("Added %s to the search engine! :D", parameters[1]);
                    } else {
                        return String.format("The given string already exists :D");
                    }
                }
            } else if (url.getPath().contains("/search")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    String list = "";
                    for (String s : words) {
                        if (s.contains(parameters[1]))
                            list += s + "\n";
                    }
                    return list;
                }
            }
            return "404 Not Found!";
        }
    }
}

class SearchEngine {
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
The `handleRequest` method simply takes in the class path, query, and fragment and then interacts wiht the backing Set of all words.

This is the main page of the web server.
[](images/lab-report-2/home.png)

To add a word to the underlying HashSet, I can add `/add?s={word}` to the path.

## Part Two: Debugging