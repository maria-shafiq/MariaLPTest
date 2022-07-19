---
title: Introduction

---
<!--Introduction-->

The process of creating and starting a simple web server in Go is easy and straightforward. 

This is a basic example:

```go
package main
 
import "net/http"
 
func indexHandler(w http.ResponseWriter, r *http.Request) {
    w.Write([]byte("<h1>Welcome to Brainarator's web server!</h1>"))
}
 
func main() {
    http.HandleFunc("/", indexHandler)
    http.ListenAndServe(":5000", nil)
}
```

In this scenario, we’ll learn how to use net/http to load and edit pages. 

More specifically, we will create an application that loads the text from a .txt file, show it on a web page. We will also create the functions to allow users to edit that file.