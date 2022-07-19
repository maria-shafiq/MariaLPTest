---
title: Handling requests and responses from a web server

---
<!--Handling requests and responses from a web server-->

Now that we have a running web server, let’s handle specific responses and requests. We’ll use the `http.HandleFunc()` method which allows us to specify how the requests we’ll be making should be handled by the selected port.

Add the code below to create a web app displaying a custom message:

Now that we have a running web server, let’s handle specific responses and requests. We’ll use the `http.HandleFunc()` method which allows us to specify how the requests we’ll be making should be handled by the selected port.

Add the code below to create a web app displaying a custom message:

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
{{copy filename='code.go'}}
```

The `http.HandleFunc()` method has two arguments, “`/`” for the route and a function of the type `http.HandlerFunc`. This function passes a value of the type `http.ResponseWriter`. It is the mechanism used for sending responses to any connected HTTP clients and also how response headers are set. The second argument is a pointer to an `http.Request` that defines how data will be retrieved from the HTTP request.


```
curl http://0.0.0.0:5000
{{ execute }}
```

Or 

```
curl http://0.0.0.0:5000/
{{ execute }}
```

Next, we’ll look at the key takeaways.