---
title: Go - Creating Web Server
date: 2024-03-26
published: true
keywords: go,web server,golang,tutorial,net,http
description: Go guide for creating simple webserver and understanding fundamentals
image: "/images/go-web-server.webp"
Tags: ["programming","golang"]
author: Hatim Master
---

## Introduction

Web servers are the backbone of the modern online world, powering everything from simple websites to complex web applications. Developers invest significant time and effort into creating robust and efficient server systems that can handle a wide range of user requests and data processing tasks. In this landscape, Go shines with its powerful standard library, which includes comprehensive support for creating HTTP web servers. Unlike some other languages, setting up a basic web server in Go is straightforward and requires minimal configuration, thanks to its built-in features for handling HTTP requests and responses.

The primary goal of this tutorial is to demystify the process of building a web server using Go and provide a solid understanding of its underlying principles. We'll start by exploring the basics of HTTP communication, including the GET and POST methods, which form the foundation of client-server interactions on the web. Through hands-on examples and practical exercises, you'll learn how to create endpoints, handle incoming requests, process data, and generate appropriate responses.

## Creating Web Server

In Go, creating a web server involves leveraging the powerful `net/http` package. The `net` package provides a portable interface for network communication, which serves as the foundation for building network applications. On top of this, the Go standard library's `http` package offers robust functionality for making HTTP requests and includes an HTTP server that can handle these requests effectively.

To kickstart the process of creating a web server in Go, we'll follow a few key steps.

1. First, we'll create a server instance that includes the desired address and port number where the server will listen for incoming requests. The HTTP server instance acts as the backbone of our web server, defining its basic configuration and communication parameters.

2. Once the HTTP server instance is set up, we'll start the server and initiate the listening process at the specified port, allowing the server to actively handle incoming HTTP requests from clients.


```go
package main

import (
    "fmt"
    "net/http"
    "log"
)


func main() {

    // Creating a server instance
    server := &http.Server{
        Addr: ":8080",
    }

    fmt.Printf("Server is starting at port 8080\n")
    err := server.ListenAndServe()
    if err != nil {
        fmt.Printf("Something went wrong when creating webserver")
        log.Fatal(err)
    }
```

The code creates an HTTP server instance (`&http.Server{}`) that listens on port 8080. It then starts the server (`server.ListenAndServe()`). If everything goes smoothly, the `ListenAndServe()` function returns `nil`, indicating that the server is running correctly.

However, if any errors occur during server startup, such as port already in use or other issues, the `ListenAndServe()` function returns a non-nil error value. In such cases, the code logs the error and exits using `log.Fatal(err)`.

In go programming there is simple version of creating server instance.The `http.ListenAndServe` function creates an HTTP server with default settings for you. It internally creates an `http.Server` instance with default configurations if you pass `nil` as the handler argument. This is a convenient way to quickly create and run a basic HTTP server without needing to explicitly create an `http.Server` object unless you need to customize the server settings (such as timeouts, TLS configuration, etc.).

```go

package main

import (
    "fmt"
    "net/http"
    "log"

)
func main() {

    fmt.Printf("Server is starting at port 8080\n")
    err := http.ListenAndServe(":8080",nil)
    if err != nil {
        fmt.Printf("Something went wrong when creating webserver")
        log.Fatal(err)
    }
}

```

In this example, `http.ListenAndServe` is used directly without creating an `http.Server` instance. The `nil` argument indicates that the default server settings should be used, making it a concise way to start a basic HTTP server in Go.

### Handling Request

In this section, we'll delve into how to make our server smart enough to handle incoming requests. Here are the key points we'll cover:

A Go HTTP server comprises two essential parts: the server itself, which listens for requests from clients, and one or more request handlers responsible for responding to these requests. Our focus will be on setting up these request handlers using `http.HandleFunc` and then starting the server using `http.ListenAndServe`.

#### Adding Request Handlers
Our server can start, but it lacks the ability to respond to requests. We'll use `http.HandleFunc` to instruct the server on which function to execute when it receives a specific type of request. This way, our server becomes equipped to respond appropriately based on the incoming requests.

**Handling Requests**: The `handleRequest` function will be pivotal here. It takes two vital parameters: `http.ResponseWriter` for sending responses back to clients and  `*http.Request` for handling incoming requests intelligently.

```go

func main() {

    fmt.Printf("Server is starting at port 8080\n")
    http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request){
        fmt.Printf("Got and Incoming Request %s\n",r.URL.Path)
        io.WriteString(w, "Hello Web!")
    })
    err := http.ListenAndServe(":8080",nil)
    if err != nil {
        fmt.Printf("Something went wrong when creating webserver")
        log.Fatal(err)
    }

```

In the above code :-

1. The `http.HandleFunc("/", ...)` line sets up a request handler for the root path ("/") of the server. When a client sends a request to the root URL, the function inside `http.HandleFunc` is executed.

2. Inside the request handler function, `func(w http.ResponseWriter, r *http.Request)`, `w `is the `http.ResponseWriter` used to send a response back to the client, and `r` is the `http.Request` object containing information about the incoming request.

## Creating Multiple Server

The flexibility of the `net/http`  package extends beyond just using your own `http.Handler`. You also have the freedom to utilize multiple HTTP servers within the same program, offering greater control and versatility in your web applications.

In this section, we'll dive into updating your program to harness the power of multiple `http.Server` instances provided by the `net/http` package. This capability becomes invaluable when you require more fine-grained control over your servers or when the need arises to manage multiple servers simultaneously within a single application.


```go
func serverOneHandler(w http.ResponseWriter,req *http.Request) {
    var html string = `
    <h1> Hello From Port 8080 </h1>
    `
        fmt.Printf("Request to / had been made by %s\n",req.Host)
        fmt.Print("Header: ",req.RequestURI)
        io.WriteString(w,html)
    }
func serverTowHandler(w http.ResponseWriter,req *http.Request) {
    var html string = `
    <h1> Hello From Port 8081 </h1>
    `
        fmt.Printf("Request to / had been made by %s\n",req.Host)
        fmt.Print("Header: ",req.RequestURI)
        io.WriteString(w,html)
    }

func main() {

    fmt.Printf("Starting Mulitple Server:\n")
    http.HandleFunc("/server",serverOneHandler)
    server := &http.Server{
        Addr: ":8080",
    }

    go func() {
        fmt.Printf("SERVER STARTED AT PORT 8080\n")
        err := server.ListenAndServe()
        if err != nil {
            fmt.Printf("Something Went wrong check log file for details")
            log.Fatal(err)
        }
    }()

    server2 := &http.Server{
        Addr: ":8081",
    }
    http.HandleFunc("/server2",serverTowHandler)

    go func() {
        fmt.Printf("SERVER STARTED AT PORT 8081\n")
        err := server2.ListenAndServe()
        if err != nil {
            fmt.Printf("Something Went wrong check log file for details")
            log.Fatal(err)
        }
    }()

    select {}
}

```

* We start by defining two handler functions: `serverOneHandler` and `serverTwoHandler`. These functions are responsible for generating responses for requests directed to different paths ("/server" and "/server2") and logging essential request details.

* Next, we create two instances of `http.Server`:`server` configured to listen on port 8080 and `server2` on port 8081. Each server is associated with its respective handler function using `http.HandleFunc`, ensuring that incoming requests to the specified paths are handled appropriately.

* The magic happens when we launch these servers concurrently using goroutines (`go func() { ... }()`). This concurrency ensures that both servers can run simultaneously, handling incoming requests independently and efficiently.

* As each server starts, a message is printed to the console confirming their initialization, along with error handling to gracefully handle any startup issues.

* Finally, we use the `select {}` statement to keep the main goroutine alive indefinitely, allowing our servers to continue running and processing requests.

## Conclusion

To sum up, the process of setting up and maintaining several HTTP servers in Go reveals the language's strong features and adaptability for web development.
With Go's concurrency features, clear handler functions, and careful error handling, we can create scalable and durable web servers that can process different kinds of requests at once.

The separation of concerns through distinct handler functions for different paths or functionalities enhances code organization and readability, while logging and error handling mechanisms ensure effective monitoring and debugging. Incorporating best practices such as graceful shutdown procedures, security considerations, and comprehensive testing further solidifies the server's reliability and resilience.

As we navigate through the intricacies of Go's net/http package and concurrency model, we unlock the potential to build sophisticated web applications with multiple server instances catering to varied requirements. With proper configuration management, documentation, and performance optimization strategies in place, our Go-powered web servers stand ready to deliver exceptional performance, security, and user experience in the ever-evolving landscape of web development.
