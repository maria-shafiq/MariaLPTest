---
title: Starting the server

---
<!--Start the server-->

Like we said in the previous step, Go uses `net/http` package to start and run a server.

This package will provide all the functions that are needed to write, request, and send HTTP requests from our program.

Now that we have a library, it's time to get our server up and running.

We do this by calling the function `http.ListenAndServe()`. This function takes two parameters:

- The port that it is serving
- An error variable.

In our case, we shall start a web server on port 5000.

Add the code below to access the necessary functions:

```go
package main
 
import "net/http"

func main() {    
	http.ListenAndServe(":5000", nil)
}
{{copy filename='code.go'}}
```

The function `http.ListenAndServe()` launches a server that takes and processes requests from port 5000.

Use the command below to start the server in the background.

```
nohup go run code.go &
{{ execute }}
```

Now, our server is running on port 5000.

To recap, we imported the `net/http` library and added `http.ListenAndServe()` to start the server after the program is run. Lastly, we started the server by running the program.

We should now have a running server locally. Verify this by following the link below:

```
curl http://0.0.0.0:5000/
{{ execute }}
```

The server will reply with a 404 response because we didn't setup the route "/". In the next steps, we’ll do that.